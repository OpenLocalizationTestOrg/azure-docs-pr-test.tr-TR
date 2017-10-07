---
title: "aaaAzure CDN kurallar altyapısı özellikleri | Microsoft Docs"
description: "Azure CDN başvuru belgelerine altyapısı eşleşme koşulları ve özellikleri kuralları."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Azure CDN kuralları özellikleri altyapısı
Merhaba kullanılabilir özelliklerin ayrıntılı açıklamaları Azure içerik teslim ağı (CDN) için bu konuda listelenmiştir [kurallar altyapısı](cdn-rules-engine.md).

Merhaba üçüncü bir kuralın parçası hello özelliğidir. Bir özellik olacak eylemin hello türünü tanımlar uygulanan bir eşleşme koşullar kümesi tarafından tanımlanan istek toohello türü.

## <a name="access"></a>Access

Bu özellikler tasarlanmış toocontrol erişim toocontent özelliklerdir.


Ad | Amaç
-----|--------
Erişimi reddet | 403 Yasak yanıtta reddedilen tüm isteği olup olmadığını belirler.
Belirteç kimlik doğrulama | Belirteç tabanlı kimlik doğrulaması uygulanan tooa isteği olup olmayacağını belirler.
Belirteç kimlik doğrulama reddi kodu | Merhaba tooToken tabanlı kimlik doğrulaması bir istek reddedildiğinde tooa kullanıcı dönen yanıtının türünü belirler.
Belirteç kimlik doğrulama URL çalışması yoksay | Belirteç tabanlı kimlik doğrulaması ile yapılan URL karşılaştırmaları büyük küçük harfe duyarlı olup olmayacağını belirler.
Belirteç kimlik doğrulama parametresi | Merhaba belirteç tabanlı kimlik doğrulaması sorgu dizesi parametresi yeniden adlandırılmış olup olmadığını belirler.

### <a name="deny-access"></a>Erişimi reddet
**Amaç**: 403 Yasak yanıtta reddedilen tüm isteği olup olmadığını belirler.

Değer | Sonuç
------|-------
Etkin| Merhaba 403 Yasak yanıtta reddetti eşleştirme ölçütü toobe karşılayan tüm isteklerin neden olur.
Devre dışı| Merhaba varsayılan davranışını geri yükler. tooallow hello kaynak sunucu toodetermine hello döndürülecek yanıt türünü Hello varsayılan davranıştır.

**Varsayılan davranış**: devre dışı

> [!TIP]
   > Bu özellik için bir olası kullanımı bir istek üst bilgisi ile eşleşen satır içi bağlantılar tooyour içeriği kullanarak koşulu tooblock erişim tooHTTP başvuran tooassociate içindir.

### <a name="token-auth"></a>Belirteç kimlik doğrulama
**Amaç:** belirteç tabanlı kimlik doğrulaması uygulanan tooa isteği olup olmayacağını belirler.

Belirteç tabanlı kimlik doğrulaması etkinleştirilirse, şifrelenmiş bir simge sağlayan ve belirtecini tarafından belirtilen toohello gereksinimlerini uyumlu yalnızca istekleri kullanılacaktır.

kullanılan tooencrypt ve şifre çözme belirteci değerler olacaktır hello şifreleme anahtarı, birincil anahtar ve belirteç kimlik doğrulama sayfasında yedekleme anahtar seçenekleri tarafından belirlenir. Şifreleme anahtarları platforma özgü göz önünde bulundurun.

Değer | Sonuç
------|---------
Etkin | Korur hello istenen içeriği belirteç tabanlı kimlik doğrulamasına sahip. Yalnızca geçerli bir belirteci sağlayan ve kendi gereksinimlerine istemcilerinden gelen istekleri kullanılacaktır. FTP hareketler belirteç tabanlı kimlik doğrulamasını bırakılır.
Devre dışı| Merhaba varsayılan davranışını geri yükler. Merhaba varsayılan davranışı tooallow bir istek güvenli belirteç tabanlı kimlik doğrulaması yapılandırma toodetermine olup.

**Varsayılan davranış:** devre dışı bırakılmış.

###<a name="token-auth-denial-code"></a>Belirteç kimlik doğrulama reddi kodu
**Amaç:** tooToken tabanlı kimlik doğrulaması bir istek reddedildiğinde tooa kullanıcı döndürülecek yanıt hello türünü belirler.

Merhaba kullanılabilir yanıt kodları aşağıda listelenmiştir.

Yanıt Kodu|Yanıt adı|Açıklama
----------------|-----------|--------
301|Kalıcı olarak taşındı|Bu durum kodu yetkisiz kullanıcıların toohello URL konumu üstbilgisinde belirtilen yönlendirir.
302|Bulunamadı|Bu durum kodu yetkisiz kullanıcıların toohello URL konumu üstbilgisinde belirtilen yönlendirir. Bir yeniden yönlendirme gerçekleştirme hello endüstri standart yöntemi bu durum kodudur.
307|Geçici yeniden yönlendirme|Bu durum kodu yetkisiz kullanıcıların toohello URL konumu üstbilgisinde belirtilen yönlendirir.
401|Yetkilendirilmemiş|Bu durum kodu WWW-Authenticate yanıt üst bilgisi ile birleştirerek tooprompt bir kullanıcı kimlik doğrulaması sağlar.
403|Yasak|Yetkisiz bir kullanıcının korumalı içeriği tooaccess çalışılırken zaman görürsünüz hello standart 403 Yasak durum iletisi budur.
404|Dosyası bulunamadı|Bu durum kodu hello HTTP istemcisi hello sunucusuyla mümkün toocommunicate kaydedildi, ancak içerik bulunamadı hello istenen gösterir.

#### <a name="url-redirection"></a>URL yeniden yönlendirme

Yapılandırılmış tooreturn 3xx durum kodu olduğunda bu özellik URL yeniden yönlendirme tooa kullanıcı tanımlı URL'sini destekler. Bu kullanıcı tarafından tanımlanan URL'yi hello aşağıdaki adımları gerçekleştirerek belirtilebilir:

1. Merhaba belirteç kimlik doğrulama reddi kod özelliği için bir 3xx yanıt kodu seçin.
2. "Konum" isteğe bağlı üstbilgi adı seçeneğini seçin.
3. İsteğe bağlı üstbilgi değeri seçeneği istenen toohello URL'sini ayarlayın.

Bir URL için 3xx durum kodu tanımlanmazsa, ardından hello 3xx durum kodu için standart yanıt sayfa toohello kullanıcı döndürülür.

URL yeniden yönlendirme yalnızca 3xx yanıt kodları için geçerlidir.

İsteğe bağlı üstbilgi değeri seçenek alfasayısal karakterler, tırnak işaretleri ve alanları destekler.

#### <a name="authentication"></a>Kimlik Doğrulaması

Bu özellik, belirteç tabanlı kimlik doğrulaması ile korunan içerik için tooan yetkisiz isteği yanıt verirken hello yetenek tooinclude WWW-Authenticate üstbilgisi destekler. WWW-Authenticate üstbilgisi "çok yapılandırmanızda temel" olarak ayarlanmış, hello yetkisiz bir kullanıcı hesabı kimlik bilgileri istenir.

Yapılandırma yukarıda Hello hello aşağıdaki adımları gerçekleştirerek elde edilebilir:

1. "401" Merhaba belirteç kimlik doğrulama reddi kod özelliği için hello yanıt kodunu seçin.
2. "WWW-Authenticate" isteğe bağlı üstbilgi adı seçeneğini seçin.
3. İsteğe bağlı üstbilgi değeri ayarı çok "temel."

WWW-Authenticate üstbilgisi yalnızca 401 yanıt kodları için geçerlidir.

### <a name="token-auth-ignore-url-case"></a>Belirteç kimlik doğrulama URL çalışması yoksay
**Amaç:** belirteç tabanlı kimlik doğrulaması ile yapılan URL karşılaştırmaları büyük küçük harfe duyarlı olup olmayacağını belirler.

Bu özellik tarafından etkilenen hello Parametreler şunlardır:

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

Geçerli değerler şunlardır:

Değer|Sonuç
---|----
Etkin|Bizim uç sunucusu URL'leri belirteç tabanlı kimlik doğrulama parametreleri için karşılaştırma tooignore durumda neden oluyor.
Devre dışı|Merhaba varsayılan davranışını geri yükler. Belirteç kimlik doğrulama toobe büyük küçük harfe duyarlı için URL karşılaştırmaları Hello varsayılan davranışı içindir.

**Varsayılan davranış:** devre dışı bırakılmış.
 
### <a name="token-auth-parameter"></a>Belirteç kimlik doğrulama parametresi
**Amaç:** hello belirteç tabanlı kimlik doğrulaması sorgu dizesi parametresi yeniden adlandırılmış olup olmadığını belirler.

Anahtar bilgileri:

- Değer seçeneği bir belirteç belirtilebilir hello sorgu dizesi parametresinin adını tanımlar.
- Değer seçeneği çok ayarlanamaz "ec_token."
- Yalnızca değer seçeneğinde tanımlanan o hello ad emin olun 
- Geçerli URL karakterler içeriyor.

Değer|Sonuç
----|----
Etkin|Değer seçeneği belirteçleri tanımlanmalıdır hello sorgu dizesi parametresinin adını tanımlar.
Devre dışı|Bir belirteç hello istek URL'si bir tanımsız sorgu dizesi parametresi olarak belirtilebilir.

**Varsayılan davranış:** devre dışı bırakılmış. Bir belirteç hello istek URL'si bir tanımsız sorgu dizesi parametresi olarak belirtilebilir.

## <a name="caching"></a>Önbelleğe alma

Bu özellikler, ne zaman ve önbelleğe alınmış içeriği nasıl tasarlanmış toocustomize özelliklerdir.

Ad | Amaç
-----|--------
Bant genişliği parametreleri | Bant genişliği azaltma parametre (yani, ec_rate ve ec_prebuf) etkin olup olmayacağını belirler.
Bant genişliği azaltma | Bizim kenar sunucuları tarafından sağlanan hello yanıt için Hello bant genişliği kısıtlar.
Önbelleği atlama | Merhaba isteği bizim önbelleğe alma teknolojisini yararlanabilirsiniz olup olmadığını belirler.
Cache-Control üstbilgisi işleme | Dış Max-Age özelliği etkin olduğunda denetimleri Cache-Control üstbilgileri nesil hello uç sunucusu tarafından hello.
Önbellek anahtarı sorgu dizesi | Merhaba önbellek anahtar eklemek veya bir istekle ilişkili sorgu dizesi parametreleri hariç belirler.
Önbellek anahtarı yeniden yazma | Merhaba önbelleği bir istekle ilişkili anahtar yeniden yazar.
Önbellek dolgu tamamlayın | Uç sunucusunda isteği sonuçları yokken Kısmi önbellek isabetsizliği ne olacağını belirler.
Sıkıştırma dosya türleri | Sıkıştırılır hello dosya biçimleri hello sunucuda tanımlar.
Varsayılan iç Max-Age | Edge sunucu tooorigin sunucu önbelleği yeniden doğrulanması için Hello varsayılan max-age aralığı belirler.
Üstbilgi işleme süresi | Merhaba dış Max-Age özelliği etkin olduğunda denetimleri bir uç sunucusu tarafından Expires üstbilgileri nesil hello.
Dış Maksimum yaş | Merhaba, max-age aralığı tarayıcı tooedge sunucusu önbellek yeniden doğrulanması için belirler.
İç Max-Age zorla | Merhaba, max-age aralığı kenar sunucu tooorigin sunucu önbelleği yeniden doğrulanması için belirler.
H.264 desteği (HTTP aşamalı indirme) | H.264 Hello tür içerik dosya kullanılan toostream olabilir biçimleri belirler.
Uy No Cache isteği | Bir HTTP istemcinin Hayır önbellek isteği toohello kaynak sunucu iletilen olup olmadığını belirler.
Kaynak No-Cache yoksay | Bizim CDN bir kaynak sunucudan sunulan belirli yönergeleri dikkate alıp almayacağını belirler.
Unsatisfiable aralıkları yoksay | Bir istek 416 İstenen aralık değil sağlanabilir durum kodu oluşturduğunda tooclients döndürülecek hello yanıtını belirler.
İç Max-eski | Önbelleğe alınan varlık sunulan hello normal sona erme süresini geçen süreyi bir kenar sunucusundan hello uç sunucusu olduğunda oluşturulamıyor toorevalidate hello hello kaynak sunucu ile önbelleğe alınmış varlık denetler.
Kısmi önbellek paylaşımı | İstek kısmen önbelleğe alınmış içeriği oluşturmak olup olmadığını belirler.
Önbelleğe alınmış içeriği prevalidate | TTL'si süresi dolmadan önce önbelleğe alınmış içeriği erken yeniden doğrulanması için uygun olup olmadığını belirler.
Sıfır bayt önbellek dosyaları Yenile | 0-bayt önbellek varlık için bir HTTP istemcinin isteğini, kenar sunucularımız nasıl işlendiğini belirler.
Önbelleğe alınabilir durum kodları | Önbelleğe alınmış içeriği sonuçlanabilir durum kodları Hello kümesini tanımlar.
Eski içerik teslim hata | Süresi dolmuş bir hata önbellek yeniden doğrulanması sırasında veya alınırken hello hello müşteri kaynak sunucudan içerik istendiğinde oluştuğunda önbelleğe alınan içerik teslim edilecek belirler.
Revalidate sırasında eski | Yeniden doğrulanması gerçekleştirilirken tooserve eski istemci toohello isteyenin kenar sunucularımızda sağlayarak performansı artırır.
Açıklama | içindeki bir kural eklenmiş bir not toobe Hello açıklama özelliği sağlar.

###<a name="bandwidth-parameters"></a>Bant genişliği parametreleri
**Amaç:** bant genişliği azaltma parametre (yani, ec_rate ve ec_prebuf) etkin olup olmayacağını belirler.

Bant genişliği azaltma parametrelerini hello veri aktarım hızı için bir istemcinin isteğini sınırlı tooa özel oranı olup olmayacağını belirler.

Değer|Sonuç
--|--
Etkin|Kenar sunucularımızda toohonor bant genişliği istekleri azaltma sağlar.
Devre dışı|Kenar sunucularımızda tooignore bant genişliği parametreleri azaltma neden olur. Merhaba, içerik (yani, bant genişliği azaltma olmadan) normal olarak sunulacak istedi.

**Varsayılan davranış:** etkin.

###<a name="bandwidth-throttling"></a>Bant genişliği azaltma
**Amaç:** kısıtlamaları hello bizim kenar sunucuları tarafından sağlanan hello yanıt için bant genişliği.

Seçenekler aşağıdaki hello her ikisi de bant genişliği azaltma yukarı ayarlamak tanımlı tooproperly olması gerekir.

Seçenek|Açıklama
--|--
KB / saniye|Kullanılan toodeliver hello yanıt olabilecek bu seçeneği toohello en yüksek bant genişliği (Kb / saniye) olarak ayarlayın.
Prebuf saniye|Bu seçenek toohello kenar sunucularımızda kadar azaltma bant genişliği bekleyeceği saniye sayısını ayarlayın. Bu süre sınırsız bant genişliği Hello amacı tooprevent takılmasını veya toobandwidth azaltma nedeniyle sorunları arabelleğe alma yaşıyor bir media player budur.

**Varsayılan davranış:** devre dışı bırakılmış.

###<a name="bypass-cache"></a>Önbelleği atlama
**Amaç:** hello isteği bizim önbelleğe alma teknolojisini yararlanabilirsiniz olup olmadığını belirler.

Değer|Sonuç
--|--
Etkin|Merhaba içerik, daha önce uç sunucularda önbelleğe olsa bile toohello kaynak sunucu üzerinden, tüm istekleri toofall neden olur.
Devre dışı|Uç sunucuların toohello önbellek İlkesi, yanıt üstbilgilerini tanımlı göre toocache varlıklar neden olur.

**Varsayılan davranış:**

- **HTTP büyük:** devre dışı

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Önbellek denetimi üstbilgisi işleme
**Amaç:** dış Max-Age özelliği etkin olduğunda Cache-Control üstbilgileri hello nesil hello uç sunucusu tarafından denetler.

Bu tür bir yapılandırma olduğundan tooplace hello dış Max-Age ve hello Cache-Control üstbilgisi işleme özelliklerinde en kolay yolu tooachieve hello hello aynı deyimi.

Değer|Sonuç
--|--
Üzerine yaz|Aşağıdaki eylemler bu hello gerçekleşecek sağlar:<br/> -Hello kaynak sunucu tarafından üretilen Cache-Control üstbilgisinin üzerine yazar. <br/>-Dış Max-Age özelliği toohello yanıt hello tarafından üretilen Cache-Control üstbilgisi ekler.
Geçirir|Merhaba dış Max-Age özelliği tarafından üretilen Cache-Control üstbilgisinin hiçbir zaman toohello yanıt eklenmesini sağlar. <br/> Cache-Control üstbilgisinin Hello kaynak sunucu neden oluyorsa toohello son kullanıcı geçer. <br/> Merhaba kaynak sunucu Cache-Control üstbilgisinin sonra bu seçeneği vermezse neden hello yanıt üstbilgisi toonot Cache-Control üstbilgisinin içerebilir.
Eksik varsa ekleyin.|Cache-Control üstbilgisinin hello kaynak sunucudan alınmadı varsa bu seçeneği hello dış Max-Age özelliği tarafından üretilen Cache-Control üstbilgisi ekler. Bu seçenek, tüm varlıklar Cache-Control üstbilgisinin atanacak sağlamak için kullanışlıdır.
Kaldır| Cache-Control üstbilgisinin hello üstbilgi yanıtıyla dahil değildir, bu seçeneği sağlar. Cache-Control üstbilgisinin zaten atanmışsa, ardından bunu hello üstbilgi yanıttan atılması.

**Varsayılan davranış:** üzerine yazın.

###<a name="cache-key-query-string"></a>Önbellek anahtarı sorgu dizesi
**Amaç:** önbellek anahtarı eklemek veya bir istekle ilişkili sorgu dizesi parametreleri hariç belirler.

Anahtar bilgileri:

- Bir veya daha fazla sorgu dizesi parametresi adları belirtin. Her parametre adı tek bir boşlukla ayrılmış.
- Bu özellik, sorgu dizesi parametreleri dahil edilecek veya hello önbellek anahtarından dışlanan olup olmadığını belirler. Her seçenek için ek bilgiler sağlanmıştır.

Tür|Açıklama
--|--
 İçerir|  Belirtilen her parametre hello önbellek anahtarında dahil olduğunu gösterir. Bu özelliği tanımlı bir sorgu dizesi parametresi için benzersiz bir değer içeren her bir istek için benzersiz bir önbellek anahtarı oluşturulur. 
 Tüm içerir  |Benzersiz sorgu dizesi içeren her isteği tooan varlık için benzersiz bir önbellek anahtar oluşturulacak gösterir. Tooa küçük İsabetli Önbellek Okuma Yüzdesi açabilir beri bu yapılandırma türü genellikle önerilmez. Daha fazla isteği tooserve gerekeceğinden bu hello kaynak sunucusundaki hello yükü artırır. Bu yapılandırma, önbelleğe alma davranışı "benzersiz önbelleği" sorgu dizesi önbelleğe alma sayfasında olarak bilinen hello çoğaltır. 
 Hariç tutma | Parametre hello önbellek anahtarından dışlanıp yalnızca o hello belirtilen gösterir. Diğer tüm sorgu dizesi parametreleri hello önbellek anahtarında dahil edilir. 
 Tüm Dışla  |Tüm sorgu dizesi parametreleri hello önbellek anahtarından hariç olduğunu gösterir. Bu yapılandırma hello varsayılan önbelleğe alma sorgu dizesi önbelleğe alma sayfasında "standart-önbellek" olarak bilinen davranışı çoğaltır. 

HTTP kurallar altyapısı Hello gücünü, sorgu dizesi önbelleğe alma uygulanır toocustomize hello şekilde sağlar. Örneğin, sorgu dizesi yalnızca Önbelleği'nün belirli konumlara veya dosya türlerini gerçekleştirilmesi belirtebilirsiniz.

Ardından tooduplicate hello sorgu dizesini önbelleğe alma davranışı "no-cache" sorgu dizesi önbelleğe alma sayfasında olarak bilinen isterseniz toocreate bir URL sorgu joker karakter eşleştirme koşul ve bir atlama önbellek özelliği içeren bir kural gerekir. Merhaba URL sorgu joker karakter eşleştirme koşulu tooan yıldız işareti (*) olarak ayarlanmalıdır.

#### <a name="sample-scenarios"></a>Örnek senaryolar

Bu özellik için örnek kullanım aşağıda verilmiştir. Önbellek anahtarı varsayılan bir örnek istek ve hello aşağıda verilmiştir.

- **Örnek istek:** http://wpc.0001.&lt; Etki alanı&gt;/800001/Origin/folder/asset.htm?sessionid=1234 & dili tr & UserID = 01 =
- **Varsayılan önbellek anahtarını:** /800001/Origin/folder/asset.htm

##### <a name="include"></a>İçerir

Örnek Yapılandırması:

- **Tür:** içerir
- **Parametre:** dili

Bu yapılandırma türü, sorgu dizesi parametresi önbellek anahtarını aşağıdaki hello oluşturur:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>Tüm içerir

Örnek Yapılandırması:

- **Tür:** tüm içerir

Bu yapılandırma türü, sorgu dizesi parametresi önbellek anahtarını aşağıdaki hello oluşturur:

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>Hariç tutma

Örnek Yapılandırması:

- **Tür:** Dışla
- **Parametre:** SessionID UserID

Bu yapılandırma türü, sorgu dizesi parametresi önbellek anahtarını aşağıdaki hello oluşturur:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>Tüm Dışla

Örnek Yapılandırması:

- **Tür:** tüm Dışla

Bu yapılandırma türü, sorgu dizesi parametresi önbellek anahtarını aşağıdaki hello oluşturur:

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>Önbellek anahtarı yeniden yazma
**Amaç:** yeniden yazdırmaya hello bir istekle ilişkili önbellek anahtarı.

Önbellek anahtarı önbelleğe alma hello amacıyla bir varlığı tanımlayan hello göreli yoldur. Diğer bir deyişle, sunucularımızda önbelleğe alınmış bir önbellek-anahtara göre tanımlanan tooits yolu göre bir varlık sürümü kontrol eder.

Bu özellik, aşağıdaki seçenekleri şu hello her ikisi de tanımlayarak yapılandırın:

Seçenek|Açıklama
--|--
Orijinal yol| Merhaba göreli yol toohello önbellek anahtarını yazılacak istek türlerini tanımlayın. Göreli bir yol, temel kaynak yolu seçerek ve ardından bir normal ifade deseni tanımlayan tanımlanabilir.
Yeni bir yol|Merhaba yeni önbellek anahtarı için göreli yol Hello tanımlayın. Göreli bir yol, temel kaynak yolu seçerek ve ardından bir normal ifade deseni tanımlayan tanımlanabilir. Bu göreli yol HTTP değişkenleri hello kullanarak dinamik olarak oluşturulabilir
**Varsayılan davranış:** bir isteğin önbellek anahtar hello isteğin URI tarafından belirlenir.

###<a name="complete-cache-fill"></a>Önbellek dolgu tamamlayın
**Amaç:** Kısmi önbellek isabetsizliği bir uç sunucusu üzerinde bir istek sonuçlanır ne olacağını belirler.

Kısmi önbellek isabetsizliği hello önbellek durumu tamamen indirilen tooan uç sunucusunu değildi bir varlık için açıklar. Bir varlığı kısmen uç sunucusunda önbelleğe alınmışsa sonra hello bu varlık için bir sonraki istekte yeniden toohello kaynak sunucuya iletilir.
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
Kısmi önbellek isabetsizliği genellikle bir kullanıcı bir indirme durdurur sonra veya yalnızca HTTP Aralık isteklerini kullanarak istenen varlıklar için oluşur. Bu özellik burada kullanıcıları genellikle bunları Başlangıç toofinish (örn., videolar) yüklemez büyük varlıkları için kullanışlıdır. Sonuç olarak, bu özellik, hello HTTP büyük platform üzerinde varsayılan olarak etkindir. Diğer tüm platformlarda devre dışı bırakılır.

Bu müşteri kaynak sunucunuzda hello yükü azaltmak ve hangi müşterilerin içeriğinizi karşıdan yükle hello hızını artırmak gerektiğinden tooleave hello varsayılan yapılandırması hello HTTP büyük platform için önerilir.

Hangi önbelleğinde ayarları izlenir toohello şekilde bu özellik eşleşme koşullar aşağıdaki hello ile ilişkili olamaz: kenar Cname, üstbilgi değişmez değer isteği, istek üstbilgisi joker, URL sorgu değişmez değer ve URL sorgu joker karakter.

Değer|Sonuç
--|--
Etkin|Merhaba varsayılan davranışını geri yükler. tooforce hello kenar sunucu tooinitiate hello varlık hello kaynak sunucusundan bir arka planda getirmeye Hello varsayılan davranıştır. Sonrasında, hello varlık hello kenar sunucunun yerel önbellekteki olacaktır.
Devre dışı|Bir uç sunucusu hello varlık için bir arka planda getirmeye gerçekleştirmesini engeller. Bu varlık o bölgesinden bir uç sunucusu toorequest neden olur bu bu hello sonraki istek anlamına gelir, hello müşteri kaynak sunucudan.

**Varsayılan davranış:** etkin.

###<a name="compress-file-types"></a>Sıkıştırma dosya türleri
**Amaç:** hello sunucuda sıkıştırılır hello dosya biçimleri tanımlar.

Bir dosya biçimi, kendi Internet medya türü (yani, Content-Type) kullanılarak belirtilebilir. Internet medya türü belirli bir varlık bizim sunucuları tooidentify hello dosya biçimini sağlar platformdan bağımsız meta verilerdir. Ortak Internet medya türleri listesi aşağıda verilmiştir.

Internet medya türü|Açıklama
--|--
Metin/düz|Düz metin dosyaları
metin/html| HTML dosyaları
metin/css|Geçişli stil sayfaları (CSS)
Uygulama/x-javascript|Javascript
Uygulama/javascript|Javascript
Anahtar bilgileri:

- Birden çok Internet medya türü, her biri tek bir boşluk ile sınırlandırma tarafından belirtin. 
- Bu özellik yalnızca, boyutu 1 MB'tan az varlıkları sıkıştırır. Daha büyük varlıklar, sunucularımız sıkıştırılmaz.
- Görüntü, video, gibi içerik ve ses ortam varlıkları (örn., JPG, MP3, MP4, vb.), belirli türde zaten sıkıştırılır. Bu tür varlıklar ek sıkıştırma önemli ölçüde dosya boyutu düşmesine değil. Bu nedenle, varlık türlerinin sıkıştırmayı etkinleştirmemeniz önerilir.
- Yıldız işareti gibi joker karakterler desteklenmez.
- Bu özellik tooa kural eklemeden önce bu kuralın uygulanacağı hello platform toowhich için sıkıştırma sayfasında sıkıştırma devre dışı seçeneğini emin tooset olun.

###<a name="default-internal-max-age"></a>Varsayılan iç Max-Age
**Amaç:** kenar sunucu tooorigin sunucu önbelleği yeniden doğrulanması için belirler hello varsayılan Maksimum yaş aralığı. Diğer bir deyişle, bir uç sunucusu önce geçecek süre miktarını hello önbelleğe alınan varlık hello kaynak sunucuda depolanan hello varlık eşleşip eşleşmediğini kontrol eder.

Anahtar bilgileri:

- Bu eylem yalnızca yanıtlar için bir kaynak sunucudan, max-age göstergesi Cache-Control veya Expires üst bilgisindeki atamadığınız gerçekleşir.
- Bu eylem bağlantısı alınabilir olarak kabul edilen olmayan varlıklar için olmayacaktır.
- Bu eylem, tarayıcı tooedge sunucusu önbellek revalidations etkilemez. Dış Max-Age özelliğiyle özelleştirilebilir toohello tarayıcı Expires üstbilgileri gönderilen veya bu tür revalidations Cache-Control tarafından belirlenir.
- Bu eylemin Hello sonuçları bir observable hello yanıt üstbilgilerini ve içeriğiniz için uç sunuculardan döndürülen hello içerik üzerinde etkisi ancak hello kenar sunucuları tooyour kaynak sunucudan gönderilen COLLECTION trafik miktarı üzerinde bir etkisi olabilir.
- Bu özellik tarafından yapılandırın:
    - Bir varsayılan iç Maksimum yaş uygulanabilir hello durum kodu seçme.
    - İstenen zaman birimi (yani, saniye, dakika, saat, vb.) bir tamsayı değeri belirterek ve ardından seçerek hello. Bu değer hello varsayılan iç max-age aralığı tanımlar.

- Ayar hello zaman birimi çok "Kapalı" bir varsayılan iç max-age aralığı Cache-Control veya Expires üst bilgisi, max-age göstergesi atanan değil istekleri için 7 gün atar.
- Hangi önbelleğinde ayarları izlenen toohello şekilde bu özellik eşleşme koşullar aşağıdaki hello ile ilişkili olamaz: 
    - Edge 
    - CNAME
    - İstek üstbilgisi değişmez değeri
    - İstek üstbilgisi joker karakter
    - İstek yöntemi
    - URL sorgu değişmez değeri
    - URL sorgu joker karakter

**Varsayılan değer:** 7 gün

###<a name="expires-header-treatment"></a>Üstbilgi işleme süresi
**Amaç:** dış Max-Age özelliği etkin olduğunda Expires üstbilgileri hello nesil bir uç sunucusu tarafından denetler.

Bu tür bir yapılandırma olduğundan tooplace hello dış Max-Age ve hello üstbilgi işleme süresi özelliklerinde en kolay yolu tooachieve hello hello aynı deyimi.

Değer|Sonuç
--|--
Üzerine yaz|Aşağıdaki eylemler bu hello gerçekleşecek sağlar:<br/>-Hello kaynak sunucu tarafından üretilen Expires üstbilgisi üzerine yazar.<br/>-Hello dış Max-Age özelliği toohello yanıt tarafından üretilen Expires üstbilgisi ekler.
Geçirir|Merhaba dış Max-Age özelliği tarafından üretilen Expires üst bilgisini hiçbir zaman toohello yanıt eklenmesini sağlar. <br/> Merhaba kaynak sunucu bir Expires üstbilgisi oluşturursa toohello son kullanıcı geçer. <br/>Merhaba kaynak sunucu bir Expires üstbilgisi sonra bu seçeneği vermezse neden hello yanıt üstbilgisi toonot Expires üst bilgisini içeriyor olabilir.
Eksik varsa ekleyin.| Expires üst bilgisi hello kaynak sunucudan alınmadı, bu seçenek hello dış Max-Age özelliği tarafından üretilen Expires üstbilgisi ekler. Bu seçenek, tüm varlıklar bir Expires üstbilgisi atanacak sağlamak için kullanışlıdır.
Kaldır| Expires üst bilgisi ile Merhaba üstbilgisi yanıt dahil değildir sağlar. Expires üst bilgisi zaten atanmışsa sonra onu hello üstbilgi yanıttan atılması.

**Varsayılan davranış:** üzerine yaz

###<a name="external-max-age"></a>Dış Maksimum yaş
**Amaç:** tarayıcı tooedge sunucusu önbellek yeniden doğrulanması için belirler hello max-age aralığı. Diğer bir deyişle, bir tarayıcı önce geçecek süre miktarını hello uç sunucusundan bir varlığı yeni bir sürümünü denetleyebilir.

Bu özelliği etkinleştirmek önbellek oluşturacağını-denetim: en fazla-geçerlilik süresi ve üstbilgileri bizim uç sunuculardan süresi dolar ve toohello HTTP istemci gönderin. Varsayılan olarak, bu üstbilgileri hello kaynak sunucu tarafından oluşturulanlar üzerine yazar. Ancak, Cache-Control üstbilgisi işleme ve üstbilgisi işleme süresi özellikleri olabilir bu davranış kullanılan tooalter olabilir.

Anahtar bilgileri:

- Bu eylem, kenar sunucu tooorigin sunucu önbelleği revalidations etkilemez. Bu tür revalidations hello kaynak sunucudan alınan önbellek-denetim/Expires üst bilgilere göre belirlenir ve varsayılan iç Max-Age ve zorla iç Max-Age özelliklerle özelleştirilebilir.
- Bu özellik bir tamsayı değeri belirterek ve hello istediğiniz zaman birimi (yani, saniye, dakika, saat, vb.) seçerek yapılandırın.
- Bu özellik tooa negatif değer saptamayı bizim kenar sunucuları toosend bir önbellek-denetimi: Hayır-önbellek ve hello ayarlamak bir süre sonu zamanı geçmişte her yanıt toohello tarayıcı ile. Bir HTTP istemcisi hello yanıt önbelleğe almaz karşın, bu ayar hello kaynak sunucudan bizim uç sunucuların özelliği toocache hello yanıt etkilemez.
- Ayar hello zaman birimi çok "Kapalı" Bu özellik devre dışı bırakır. Merhaba kaynak sunucu Hello yanıtıyla önbelleğe önbellek-denetim/Expires üstbilgileri toohello tarayıcı üzerinden geçer.

**Varsayılan davranış:** devre dışı

###<a name="force-internal-max-age"></a>İç Max-Age zorla
**Amaç:** kenar sunucu tooorigin sunucu önbelleği yeniden doğrulanması için belirler hello max-age aralığı. Diğer bir deyişle, bir uç sunucusu önce geçecek süre miktarını hello önbelleğe alınan varlık hello kaynak sunucuda depolanan hello varlık eşleşip eşleşmediğini kontrol edebilirsiniz.

Anahtar bilgileri:

- Bu özellik hello max-age aralığı Cache-Control veya bir kaynak sunucudan oluşturulan Expires üstbilgileri tanımlı geçersiz kılar.
- Bu özellik, tarayıcı tooedge sunucusu önbellek revalidations etkilemez. Expires üstbilgileri toohello tarayıcı gönderilen veya bu tür revalidations Cache-Control tarafından belirlenir.
- Bu özellik bir uç sunucusu toohello istek sahibi tarafından teslim hello yanıt gözlemlenebilir bir etkisi yok. Bununla birlikte, bizim kenar sunucuları toohello kaynak sunucudan gönderilen COLLECTION trafik miktarı hello üzerinde bir etkisi olabilir.
- Bu özellik tarafından yapılandırın:
    - Bir iç max-age uygulanacak hello durum kodu seçme.
    - Bir tamsayı değeri belirterek ve seçmek istediğiniz zaman birimi (yani, saniye, dakika, saat, vb.) hello. Bu değer hello isteğin max-age aralığı tanımlar.

- Ayar hello zaman birimi çok "Kapalı" Bu özellik devre dışı bırakır. Bir iç max-age aralık toorequested varlıklar atanmamış. Merhaba özgün üstbilgisi önbelleğe alma yönergeleri içermiyorsa, ardından hello varlık toohello etkin ayarı varsayılan iç Max-Age özelliği göre önbelleğe alınır.
- Hangi önbelleğinde ayarları izlenen toohello şekilde bu özellik eşleşme koşullar aşağıdaki hello ile ilişkili olamaz: 
    - Edge 
    - CNAME
    - İstek üstbilgisi değişmez değeri
    - İstek üstbilgisi joker karakter
    - İstek yöntemi
    - URL sorgu değişmez değeri
    - URL sorgu joker karakter

**Varsayılan davranış:** devre dışı

###<a name="h264-support-http-progressive-download"></a>H.264 desteği (HTTP aşamalı indirme)
**Amaç:** H.264 belirler hello türleri kullanılan toostream olabilir biçimleri içerik dosyası.

Anahtar bilgileri:

- İzin verilen H.264 dosya adı uzantıları boşlukla ayrılmış bir dizi dosya uzantılarını seçeneğinde tanımlayın. Dosya uzantıları seçeneği hello varsayılan davranışı geçersiz kılar. Bu dosya adı uzantıları dahil ederek, bu seçeneği ayarlarken MP4 ve F4V desteği korur. 
- Bir nokta emin tooinclude olun her dosya adı uzantısı (örn., .mp4 .f4v) belirtirken.

**Varsayılan davranış:** HTTP aşamalı indirme MP4 ve F4V medya varsayılan olarak destekler.

###<a name="honor-no-cache-request"></a>Uy Hayır önbellek isteği
**Amaç:** toohello kaynak sunucu bir HTTP istemcinin Hayır önbellek isteği iletilen olup olmadığını belirler.

Hayır önbellek isteği Hello HTTP istemci önbellek gönderdiğinde oluşur-denetim: Hayır-önbellek ve/veya Pragma:no-cache üstbilgisi hello HTTP isteği.

Değer|Sonuç
--|--
Etkin|Bir HTTP istemcinin no-cache toobe iletilen toohello kaynak sunucu isteklerini ve hello kaynak sunucuya geri toohello HTTP istemci hello yanıt üstbilgilerini ve hello gövde hello uç sunucusu üzerinden döndürür sağlar.
Devre dışı|Merhaba varsayılan davranışını geri yükler. toohello kaynak sunucu iletilen gelen tooprevent Hayır önbellek isteği Hello varsayılan davranıştır.

Tüm üretim trafiği için yüksek oranda olmasından tooleave bu özellik, varsayılan devre dışı durumunda önerilir. Aksi halde, kaynak sunucuları birçok Hayır önbellek isteği web sayfaları yenilerken yanlışlıkla tetikleyebilir son kullanıcılardan korumalı değil veya hello olan birçok popüler medya oynatıcıları toosend no cache üstbilgisi video her istekle kodlanmış. Bununla birlikte, bu özellik kullanışlı tooapply toocertain üretim dışı hazırlama olabilir veya isteğe bağlı hello kaynak sunucudan çekilen dizinleri, sipariş tooallow yeni içerik toobe içinde test.

iletilen toobe tooan kaynak sunucu toothis özelliği son TCP_Client_Refresh_Miss verilen bir istek için bildirilen hello önbellek durumu. Merhaba çekirdek raporlama modülünde kullanılabilir önbellek durumları rapor istatistiksel bilgileri önbelleği durumuna göre sağlar. Bu, tootrack hello numarası ve tooan kaynak sunucu toothis özelliği son iletilen istekleri yüzdesini sağlar.

**Varsayılan davranış:** devre dışı bırakılmış.

###<a name="ignore-origin-no-cache"></a>Kaynak no-cache yoksay
**Amaç:** bizim CDN bir kaynak sunucudan sunulan yönergeleri izleyerek hello dikkate alıp almayacağını belirler:

- Cache-Control: özel
- Cache-Control: no-store
- Cache-Control: no-cache
- Pragma: no-cache

Anahtar bilgileri:

- Bu özellik, yukarıdaki yönergeleri hello yoksayılacak durum kodları boşlukla ayrılmış bir listesi tanımlayarak yapılandırın.
- Merhaba bu özellik için geçerli durum kodları kümesidir: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 ve 505.
- Bu özellik tooa boş değerine ayarlayarak devre dışı bırakın.
- Hangi önbelleğinde ayarları izlenen toohello şekilde bu özellik eşleşme koşullar aşağıdaki hello ile ilişkili olamaz: 
    - Edge 
    - CNAME
    - İstek üstbilgisi değişmez değeri
    - İstek üstbilgisi joker karakter
    - İstek yöntemi
    - URL sorgu değişmez değeri
    - URL sorgu joker karakter

**Varsayılan davranış:** toohonor hello yukarıdaki yönergeleri varsayılan davranıştır.

###<a name="ignore-unsatisfiable-ranges"></a>Unsatisfiable aralıkları yoksay 
**Amaç:** bir istek 416 İstenen aralık değil sağlanabilir durum kodu oluşturduğunda, tooclients döndürülen hello yanıtını belirler.

Merhaba bayt aralığı isteği bir uç sunucusu tarafından karşılanamayan ve IF-Range isteği üstbilgisi alanının belirtilmedi belirtildiğinde varsayılan olarak, bu durum kodu döndürülür.

Değer|Sonuç
-|-
Etkin|Kenar sunucularımızda bir 416 İstenen aralık değil sağlanabilir durum koduyla yanıt veren tooan geçersiz bayt aralığı isteğinden engeller. Bunun yerine sunucularımızda hello istenen varlık teslim etmek ve bir 200 Tamam hello istemciye döndür.
Devre dışı|Merhaba varsayılan davranışını geri yükler. toohonor 416 İstenen aralık değil sağlanabilir durum kodu Hello varsayılan davranıştır.

**Varsayılan davranış:** devre dışı bırakılmış.

###<a name="internal-max-stale"></a>İç Max-eski
**Amaç:** önbelleğe alınan varlık sunulan bir kenar sunucusundan hello uç sunucusu oluşturamıyor toorevalidate hello olduğunda son hello normal sona erme zamanı varlık hello kaynak sunucu ile ne kadar süreyle önbelleğe denetler.

Normalde, bir varlığın, max-age süresi dolduğunda, hello uç sunucusunu bir COLLECTION toohello kaynak sunucu isteği gönderir. Merhaba kaynak sunucu sonra ile ya da bir 304 yanıtlar hello uç sunucusu yeni bir kira hello önbelleğe alınan varlık üzerinde or else 200 Tamam hello uç sunucusu ile Merhaba önbelleğe alınan varlık güncelleştirilmiş bir sürümünü sağlayın sağlamak için değiştirilemez.

Merhaba uç sunucusu oluşturamıyor tooestablish böyle bir COLLECTION çalışırken hello kaynak sunucu ile bağlantı ise, bu dahili Max eski özelliği olup olmadığı ve ne kadar hello için uç sunucusunu tooserve hello şimdi eski varlık devam edebilirsiniz denetler.

Merhaba varlığın max-age dolduğunda değil hello başarısız COLLECTION oluştuğunda, bu zaman aralığı başlatır. Bu nedenle, hello en uzun süresi boyunca başarılı COLLECTION bir varlık sunulabilen hello hello birleşimi, max-age artı max eski tarafından belirtilen zaman miktarıdır. Başarısız bir COLLECTION denemesi sırasında daha sonra bir varlık 9:00 30 dakika cinsinden maksimum yaş ve en çok eski 15 dakika ile önbelleğe alınmışsa 9:46 başarısız COLLECTION teşebbüs neden olacağından sırada Örneğin, 9:44 bir son kullanıcı alıcı hello eski önbelleğe alınan varlığı, neden olur Merhaba son kullanıcı 504 ağ geçidi zaman aşımı alma.

Bu özellik önbelleği tarafından değiştirilen için yapılandırılan herhangi bir değer-denetim: gereken-düzeltin veya önbellek-denetimi: proxy-hello kaynak sunucudan alınan üstbilgileri düzeltin. Bu üstbilgiler birini alındığında, hello kaynak sunucudan bir varlık başlangıçta önbelleğe alındığında sonra hello uç sunucu eski bir önbelleğe alınan varlık hizmet vermeyecek. Hello uç sunucusu oluşturamıyor toorevalidate hello kaynağına sahip ise Hello varlığın, max-age aralığı sona erdiğinde, böyle bir durumda hello uç sunucu 504 ağ geçidi zaman aşımı sonra döndürür.

Anahtar bilgileri:

- Bu özellik tarafından yapılandırın:
    - Seçme hello durum kodu max eski uygulanır.
    - İstenen zaman birimi (yani, saniye, dakika, saat, vb.) bir tamsayı değeri belirterek ve ardından seçerek hello. Bu değer hello iç max-uygulanacak olan eski tanımlar.

- Ayar hello zaman birimi çok "Kapalı" Bu özellik devre dışı bırakır. Önbelleğe alınan bir varlık, kendi normal sona erme zamanı sunulmayacak.
- Hangi önbelleğinde ayarları izlenen toohello şekilde bu özellik eşleşme koşullar aşağıdaki hello ile ilişkili olamaz: 
    - Edge 
    - CNAME
    - İstek üstbilgisi değişmez değeri
    - İstek üstbilgisi joker karakter
    - İstek yöntemi
    - URL sorgu değişmez değeri
    - URL sorgu joker karakter

**Varsayılan davranış:** 2 dakika

###<a name="partial-cache-sharing"></a>Kısmi önbellek paylaşımı
**Amaç:** istek kısmen önbelleğe alınmış içeriği oluşturmak olup olmadığını belirler.

İçerik tam olarak önbelleğe Hello istenen kadar bu kısmi önbellek sonra bu içerik için kullanılan toofulfill yeni istekleri olabilir.

Değer|Sonuç
-|-
Etkin|İstekleri kısmen önbelleğe alınmış içeriği oluşturabilirsiniz.
Devre dışı|İstekleri yalnızca tam olarak önbelleğe alınmış üretebilir hello sürümünü içerik istedi.

**Varsayılan davranış:** devre dışı bırakılmış.

###<a name="prevalidate-cached-content"></a>Önbelleğe alınmış içeriği prevalidate
**Amaç:** TTL'si süresi dolmadan önce önbelleğe alınmış içeriği erken yeniden doğrulanması için uygun olup olmadığını belirler.

Merhaba süreyi hello önceki toohello sona erme tarihi, erken yeniden doğrulanması uygun olacağı içeriğinin TTL istedi tanımlayın.

Anahtar bilgileri:

- Önbelleğe alınmış hello içeriğinin TTL süresi dolduktan sonra "Kapalı" Merhaba zaman birimi seçerek yeniden doğrulanması tootake yer gerektirir. Zaman belirtilmemesi gerekir ve göz ardı edilir.

**Varsayılan davranış:** devre dışı. Yeniden doğrulanması yalnızca sonra önbelleğe alınan içeriğin TTL süresi doldu hello yer alabilir.

###<a name="refresh-zero-byte-cache-files"></a>Sıfır bayt önbellek dosyaları Yenile
**Amaç:** 0 bayt önbellek varlık için bir HTTP istemcinin isteğini, kenar sunucularımız nasıl işlendiğini belirler.

Geçerli değerler şunlardır:

Değer|Sonuç
--|--
Etkin|Bizim kenar sunucu toore fetch hello varlık hello kaynak sunucudan neden olur.
Devre dışı|Merhaba varsayılan davranışını geri yükler. istek üzerine geçerli önbellek varlıklar yukarı tooserve Hello varsayılan davranıştır.
Bu özellik doğru önbelleğe alma ve içerik dağıtımı için gerekli değildir, ancak geçici bir çözüm olarak yararlı olabilir. Örneğin, kaynak sunucularda dinamik içerik oluşturucuları yanlışlıkla 0 baytlık yanıtları toohello uç sunucuların gönderilen neden olabilir. Bu tür yanıtları genellikle, kenar sunucularımız önbelleğe alınır. 0-bayt yanıt hiçbir zaman geçerli bir yanıt olduğunu biliyorsanız 

Bu tür içerik için daha sonra bu özellik Varlık türlerinin tooyour istemciler hizmet engelleyebilir.

**Varsayılan davranış:** devre dışı bırakılmış.

###<a name="set-cacheable-status-codes"></a>Önbelleğe alınabilir durum kodları
**Amaç:** önbelleğe alınmış içeriği sonuçlanabilir durum kodları hello kümesini tanımlar.

Varsayılan olarak, önbelleğe alma 200 Tamam yanıtlar için yalnızca etkinleştirilir.

İstenen hello durum kodları boşlukla ayrılmış bir kümesini tanımlar.

Anahtar bilgileri:

- Lütfen Kaynak No-Cache yoksay özelliği de etkinleştirin. Bu özellik etkin değilse, ardından 200 Tamam yanıtlarını önbelleğe değil.
- Merhaba bu özellik için geçerli durum kodları kümesidir: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 ve 505.
- Bu özellik bir 200 Tamam durum kodu oluşturan yanıtlar için önbelleğe alma kullanılan toodisable olamaz.

**Varsayılan davranış:** önbelleğe alma 200 Tamam durum kodu oluşturan yanıtlar için yalnızca etkin.
###<a name="stale-content-delivery-on-error"></a>Eski içerik teslim hata
**Amaç:** 

Süresi dolmuş bir hata önbellek yeniden doğrulanması sırasında veya alınırken hello hello müşteri kaynak sunucudan içerik istendiğinde oluştuğunda önbelleğe alınan içerik teslim edilecek belirler.

Değer|Sonuç
-|-
Etkin|Bir bağlantı tooan kaynak sunucu sırasında bir hata oluştuğunda, eski içerik toohello isteyenin sunulacak.
Devre dışı|Merhaba kaynak sunucunun hata toohello isteyenin iletilir.

**Varsayılan davranış:** devre dışı

###<a name="stale-while-revalidate"></a>Revalidate sırasında eski
**Amaç:** COLLECTION gerçekleştirilirken tooserve eski içerik toohello isteyenin kenar sunucularımızda sağlayarak performansı geliştirir.

Anahtar bilgileri:

- Bu özellik Hello davranışını according toohello seçilen zaman birimi değişir.
    - **Zaman birimi:** bir zaman birimi (örn., saniye, dakika, saat, vb.) tooallow eski içerik teslim seçin ve bir süre belirtin. Bu tür kurulum hello CDN tooextend hello süreyi teslim edebilir formülü aşağıdaki toohello göre doğrulama istemeden önce içerik verir:**TTL** + **eski sırada düzeltin zaman** 
    - **Kapalı:** eski içerik sunulması "Kapalı" istek önce toorequire COLLECTION seçin.
        - Uygulanamaz ve yok sayılacak bu yana bir süre boyunca belirtmeyin.

**Varsayılan davranış:** devre dışı. İçerik sunulması Hello istenen önce yeniden doğrulanması gerçekleşmesi gerekir.

###<a name="comment"></a>Açıklama
**Amaç:** içindeki bir kural eklenmiş bir not toobe sağlar.

Bu özellik için bir kullanım hello genel amaçlı bir kuralın hakkında ek bilgi tooprovide ya da belirli bir neden eşleşen koşulu veya özellik toohello kuralı eklendi.

Anahtar bilgileri:

- En fazla 150 karakter belirtilebilir.
- Alfasayısal karakterler kullanın emin tooonly olun.
- Bu özellik hello kural hello davranışını etkilemez. Ayrıca, ileride veya, bilgiler nerede sağlayabilir bir alanı hello kural gidermede yardımcı olabilecek tooprovide yalnızca amaçlanmıştır.
 
## <a name="headers"></a>Üstbilgileri

Bu özellikler tasarlanmış tooadd olan, değiştirmek veya hello istek veya yanıt üstbilgileri silmek.

Ad | Amaç
-----|--------
Age yanıtı üstbilgisi | Age yanıtı üstbilgisi toohello isteyenin gönderilen hello yanıta dahil edilip edilmeyeceğini belirler.
Önbellek yanıt üstbilgilerini hata ayıklama | Bir yanıt hello istenen varlık için hello önbellek İlkesi hakkında bilgi sağlayan hello X EC Debug yanıt üstbilgisi içerebilir olup olmadığını belirler.
İstemci istek üstbilgisi değiştirme | Geçersiz kılar, ekler veya bir istekten bir üstbilgi siler.
İstemci yanıt üstbilgisi değiştirme | Geçersiz kılar, ekler veya bir yanıt üstbilgi siler.
İstemci IP özel üstbilgi ayarlayın | Merhaba isteyen istemcinin IP adresini Hello toobe eklenen toohello istek özel istek üstbilgisi olarak sağlar.

###<a name="age-response-header"></a>Age yanıtı üstbilgisi
**Amaç**: Age yanıtı üstbilgisi hello gönderilen yanıtı toohello tanımlanırken dahil edilip edilmeyeceğini belirler.
Değer|Sonuç
--|--
Etkin | Merhaba Age yanıtı üstbilgisi toohello isteyenin gönderilen hello yanıt olarak dahil edilir.
Devre dışı | Merhaba Age yanıtı üstbilgisi toohello isteyenin gönderilen hello yanıttan edilmeyecek.

**Varsayılan davranış**: devre dışı bırakılmış.

###<a name="debug-cache-response-headers"></a>Önbellek yanıt üstbilgilerini hata ayıklama
**Amaç:** yanıt hello istenen varlık için hello önbellek İlkesi hakkında bilgi sağlayan X EC Debug yanıt üstbilgisi içerebilir olup olmadığını belirler.

Önbellek yanıtı hello aşağıdaki her ikisi de true olduğunda hello yanıtta üstbilgileri dahil edilecek hata ayıklama:

- hello istenen isteğinde Hello hata ayıklama önbellek yanıt üstbilgileri özelliği etkinleştirildi.
- İstek yukarıda Hello hello yanıta dahil edilmesini hata ayıklama önbellek yanıt üstbilgilerini hello kümesini tanımlar.

Üstbilgi üstbilgi aşağıdaki hello dahil ederek istenebilir ve istenen yönergeleri hello isteğindeki hello önbellek yanıtı hata ayıklama:

X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_

**Örnek:**

X EC Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

Değer|Sonuç
-|-
Etkin|Hata ayıklama önbellek yanıt üstbilgileri için istekleri X EC Debug üstbilgi içeren bir yanıt döndürür.
Devre dışı|X EC Debug yanıt üstbilgisi hello yanıttan edilmeyecek.

**Varsayılan davranış:** devre dışı bırakılmış.

###<a name="modify-client-response-header"></a>İstemci yanıt üstbilgisi değiştirme
**Amaç:** her istek bir dizi içeriyor [istek üst]() onu açıklayan. Bu özellik şunlardan birini yapabilirsiniz:

- Append veya tooa istek üstbilgisi atanan hello değer üzerine yazabilirsiniz. Ardından Hello belirtilen istek üstbilgisi mevcut değilse, bu özellik, toohello isteği ekleyeceksiniz.
- Bir istek üstbilgisini hello isteğinden silin.

Tooan kaynak sunucu iletilen istekleri bu özellik tarafından yapılan hello değişiklikleri yansıtır.

Aşağıdaki eylemler hello birini istek üst bilgisinde gerçekleştirilebilir:

Seçenek|Açıklama|Örnek
-|-|-
Ekle|Hello hello varolan istek üstbilgi değerinin toend katma değer belirtilmiş.|**Üstbilgi değeri (istemci) istek:**Value1 <br/> **Üstbilgi değeri (HTTP kurallar altyapısı) istek:** Value2 <br/>**Yeni istek üstbilgi değeri:** Value1Value2
Üzerine yaz|Belirtilen değer hello isteği üstbilgi değeri kümesi toohello olacaktır.|**Üstbilgi değeri (istemci) istek:**Value1 <br/>**Üstbilgi değeri (HTTP kurallar altyapısı) istek:** Value2 <br/>**Yeni istek üstbilgi değeri:** Value2 <br/>
Sil|Merhaba belirtilen istek üstbilgisi siler.|**Üstbilgi değeri (istemci) istek:**Value1 <br/> **İstemci istek üstbilgisi yapılandırmasını Değiştir:** Delete hello istek üstbilgisi söz konusu. <br/>**Sonuç:** hello belirtilen istek üstbilgisi toohello kaynak sunucu değil iletilir.

Anahtar bilgileri:

- Merhaba değer adı seçeneğinde belirtilen hello istenen istek üstbilgisi için tam bir eşleşme olduğundan emin olun.
- Servis talebi üstbilgi tanımlamanın hello amaçla dikkate alınmaz. Örneğin, Cache-Control üstbilgisi adı varyasyonları aşağıdaki hello hiçbirini kullanılan tooidentify olabilir:
    - ön bellek denetimi
    - CACHE-CONTROL
    - cachE-Control
- Bir üstbilgi adı belirtirken alfasayısal karakterler, tire ve alt çizgi kullanmanız emin tooonly olun.
- Üstbilgi silme tooan kaynak sunucu kenar sunucularımızda tarafından iletilen engeller.
- Merhaba aşağıdaki üst bilgiler ayrılmış ve bu özellik tarafından değiştirilemez:
    - iletilen
    - ana bilgisayar
    - aracılığıyla
    - Uyarı
    - x-iletilen-için
    - "X-AB" ile başlayan tüm başlığı adları ayrılmıştır.

###<a name="modify-client-response-header"></a>İstemci yanıt üstbilgisi değiştirme
Her yanıtı kümesini içeren [yanıt üstbilgilerini]() onu açıklayan. Bu özellik şunlardan birini yapabilirsiniz:

- Append veya tooa yanıt üstbilgisi atanan hello değer üzerine yazabilirsiniz. Ardından Hello belirtilen istek üstbilgisi mevcut değilse, bu özellik, toohello yanıt ekleyeceksiniz.
- Bir yanıt üstbilgisi hello yanıttan silin.

Varsayılan olarak, yanıt üstbilgi değerleri, bir kaynak sunucu ve kenar sunucularımızda tarafından tanımlanır.

Aşağıdaki eylemler hello birini bir yanıt üstbilgisi gerçekleştirilebilir:

Seçenek|Açıklama|Örnek
-|-|-
Ekle|Hello hello varolan istek üstbilgi değerinin toend katma değer belirtilmiş.|**Yanıt üstbilgi değeri (istemci):**Value1 <br/> **Yanıt üstbilgi değeri (HTTP kurallar altyapısı):** Value2 <br/>**Yeni yanıt üstbilgi değeri:** Value1Value2
Üzerine yaz|Belirtilen değer hello isteği üstbilgi değeri kümesi toohello olacaktır.|**Yanıt üstbilgi değeri (istemci):**Value1 <br/>**Yanıt üstbilgi değeri (HTTP kurallar altyapısı):** Value2 <br/>**Yeni yanıt üstbilgi değeri:** Value2 <br/>
Sil|Merhaba belirtilen istek üstbilgisi siler.|**Üstbilgi değeri (istemci) istek:** Value1 <br/> **İstemci isteği üstbilgisi yapılandırmasını Değiştir:** Delete hello yanıt üstbilgisi söz konusu. <br/>**Sonuç:** hello belirtilen yanıt üstbilgisi toohello istek sahibi değil iletilir.

Anahtar bilgileri:

- Merhaba değer adı seçeneğinde belirtilen hello istenen yanıt üstbilgisi için tam bir eşleşme olduğundan emin olun. 
- Servis talebi üstbilgi tanımlamanın hello amaçla dikkate alınmaz. Örneğin, Cache-Control üstbilgisi adı varyasyonları aşağıdaki hello hiçbirini kullanılan tooidentify olabilir:
    - ön bellek denetimi
    - CACHE-CONTROL
    - cachE-Control
- Üstbilgi silme toohello isteyenin iletilen engeller.
- Merhaba aşağıdaki üst bilgiler ayrılmış ve bu özellik tarafından değiştirilemez:
    - kabul kodlama
    - geçerlilik süresi
    - bağlantı
    - İçerik kodlama
    - içerik uzunluğu
    - İçerik aralığı
    - Tarih
    - sunucu
    - toplamı
    - Transfer-encoding
    - Yükseltme
    - değişir
    - aracılığıyla
    - Uyarı
    - "X-AB" ile başlayan tüm başlığı adları ayrılmıştır.

###<a name="set-client-ip-custom-header"></a>İstemci IP özel üstbilgi ayarlayın
**Amaç:** hello isteyen istemci IP adresi toohello isteğiyle tanımlayan bir özel üst bilgi ekler.

Üstbilgi adı seçeneği hello istemcinin IP adresi depolanacağı hello özel istek üstbilgisi hello adını tanımlar.

Bu özellik, bir müşteri kaynak sunucu toofind özel istek üstbilgisi aracılığıyla istemci IP adresleri çıkışı sağlar. Merhaba isteği önbellekten sunan, hello kaynak sunucu hello istemcinin IP adresini bildirilmez. Bu nedenle, bu özellik ADN veya önbelleğe alınmaz varlıklar ile kullanılması önerilir.

Lütfen bu hello belirtilen üstbilgi adı hello aşağıdakilerden herhangi birini eşleşmiyor emin olun:

- Standart istek üstbilgisi adları. Standart üstbilgi adlarının bir listesini bulunabilir [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).
- Ayrılmış üstbilgi adları:
    - iletilen için
    - ana bilgisayar
    - değişir
    - aracılığıyla
    - Uyarı
    - x-iletilen-için
    - "X-AB" ile başlayan tüm başlığı adları ayrılmıştır.
 
## <a name="logs"></a>Günlükler

Bu özelliklerin ham günlük dosyalarında saklanan tasarlanmış toocustomize hello verilerdir.

Ad | Amaç
-----|--------
Özel günlük alanı 1 | Merhaba biçimi ve ham günlük dosyasında toohello özel günlük alan atanacak hello içerik belirler.
Günlük sorgu dizesi | Bir sorgu dizesi erişim günlükleri hello URL'de birlikte depolanan olup olmadığını belirler.

###<a name="custom-log-field-1"></a>Özel günlük alanı 1
**Amaç:** hello biçimi ve ham günlük dosyasında toohello özel günlük alan atanacak hello içeriği belirler.

Bu özel alan arkasında Hello ana amacı olan tooallow hangi istek ve yanıt üstbilgi değerleri, günlük dosyalarında depolanacağı toodetermine.

Varsayılan olarak, hello özel günlük alan "x-ec_custom-1." olarak adlandırılır Ancak, bu alanı hello adını özelleştirilebilecek [ham günlük ayarları sayfası]().

toospecify istek ve yanıt üstbilgileri kullanması gereken biçimlendirme hello aşağıda tanımlanmıştır.

Üstbilgi türü|Biçimi|Örnekler
-|-|-
İstek üstbilgisi|%{[RequestHeader]()}[t]() | % {Kabul-Encoding} t <br/> {Başvuran} t <br/> % {Yetkilendirme} i
Yanıt Üst Bilgisi|%{[ResponseHeader]()}[o]()| % {Yaş} o <br/> % {Content-Type} o <br/> % {Tanımlama bilgisi} o

Anahtar bilgileri:

- Özel günlük alan üstbilgi alanları ve düz metin herhangi bir birleşimini içerebilir.
- Bu alanın geçerli karakterler hello aşağıdakileri içerir: alfasayısal (yani, 0-9, a-z ve A-Z), tire, iki nokta üst üste, noktalı, kesme, virgül, nokta, alt çizgi, eşittir işareti, parantez, köşeli ayraçlar ve boşluk. Merhaba yüzdesi simge ve süslü ayraçlar yalnızca ne zaman izin verilir toospecify üstbilgi alanı kullanılır.
- Her belirtilen üstbilgi alanı Hello yazım hello istenen istek/yanıt üstbilgisi adı eşleşmelidir.
- Toospecify isterseniz birden çok üst bilgileri, sonra da önerilir ayırıcı tooindicate her üstbilgiyi kullanır. Örneğin, her başlığı için bir kısaltma kullanabilirsiniz. Örnek sözdizimi aşağıda verilmiştir.
    - AE: % {kabul-Encoding} i A: % {Yetkilendirme} i u: % {Content-Type} o 

**Varsayılan değer:** -

###<a name="log-query-string"></a>Günlük sorgu dizesi
**Amaç:** bir sorgu dizesi erişim günlükleri hello URL'de birlikte depolanan olup olmadığını belirler.

Değer|Sonuç
-|-
Etkin|Sorgu dizeleri Hello depolanmasını URL'leri bir erişim günlüğe kaydederken sağlar. Bir URL bir sorgu dizesi içermiyorsa, sonra bu seçeneği bir etkisi olmayacaktır.
Devre dışı|Merhaba varsayılan davranışını geri yükler. Merhaba varsayılan tooignore sorgu dizeleri URL'leri bir erişim günlüğe kaydederken bir davranıştır.

**Varsayılan davranış:** devre dışı bırakılmış.

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>Kaynak

Bu özellikler hello CDN kaynak sunucu ile nasıl iletişim kurduğu tasarlanmış toocontrol özelliklerdir.

Ad | Amaç
-----|--------
En fazla tutma isteği | Kapalı olduğu önce hello en fazla istek tutma bağlantı sayısını tanımlar.
Proxy özel üstbilgileri | Bir uç sunucusu tooan kaynak sunucusundan iletilen CDN özgü istek üstbilgileri Hello kümesini tanımlar.


###<a name="maximum-keep-alive-requests"></a>En fazla tutma isteği
**Amaç:** , kapatılmış olmasından önce hello en fazla istek tutma bağlantı sayısını tanımlar.

Merhaba istekleri tooa düşük değer en fazla sayısını ayarlama kesinlikle önerilmez ve performans düşüşüne neden olabilir.

Anahtar bilgileri:

- Bu değer bir tamsayı belirtin.
- Virgül veya nokta belirtilen hello içermez değeri.

**Varsayılan değer:** 10.000 istekleri

###<a name="proxy-special-headers"></a>Proxy özel üstbilgileri
**Amaç:** hello kümesini tanımlayan [CDN özgü istek üstbilgileri]() bir uç sunucusu tooan kaynak sunucudan iletilir.

Anahtar bilgileri:

- Bu özellik tanımlanan her CDN özgü istek üstbilgisi tooan kaynak sunucuya iletilir.
- CDN özel istek üstbilgisi tooan kaynak sunucuyu bu listeden kaldırarak iletilmelerini önleyebilirsiniz.

**Varsayılan davranış:** tüm [CDN özgü istek üstbilgileri]() toohello kaynak sunucuya iletilir.

## <a name="specialty"></a>Özel

Bu özellikler yalnızca gelişmiş kullanıcılar tarafından kullanılması gereken gelişmiş işlevsellik sağlar.

Ad | Amaç
-----|--------
Önbelleğe alınabilir HTTP yöntemleri | Merhaba bizim ağ üzerinde önbelleğe ek HTTP yöntemleri kümesini belirler.
Önbelleğe alınabilir istek gövdesi boyutu | Bir POST yanıt önbelleğe olup olmadığını belirlemek için hello eşiğini tanımlar.

###<a name="cacheable-http-methods"></a>Önbelleğe alınabilir HTTP yöntemleri
**Amaç:** hello bizim ağ üzerinde önbelleğe ek HTTP yöntemleri kümesini belirler.

Anahtar bilgileri:

- Bu özellik GET yanıtları her zaman önbelleğe alınacağını varsayar. Sonuç olarak, hello GET HTTP yöntemini bu özelliği ayarlanırken dahil olmamalıdır.
- Bu özellik yalnızca hello POST HTTP yöntemini destekler. Bu özellik ayarlayarak POST yanıt önbelleğe almayı etkinleştir: POST 
- Varsayılan olarak, yalnızca, gövde 14 KB'den küçük istekleri önbelleğe alınır. Merhaba en büyük istek gövdesi boyutunu ayarlamak için alınabilir istek gövdesi boyutu özelliğini kullanın.

**Varsayılan davranış:** yalnızca GET yanıtlarını önbelleğe alınır.

###<a name="cacheable-request-body-size"></a>Önbelleğe alınabilir istek gövdesi boyutu

**Amaç:** POST yanıt önbelleğe olup olmadığını belirlemek için hello eşik tanımlar.

Bu eşik en büyük istek gövdesi boyutu belirterek belirlenir. Daha büyük bir istek gövdesini içeren istekleri önbelleğe alınmamış.

Anahtar bilgileri:

- Bu özellik yalnızca POST yanıtlarını önbelleğe alma işlemi için uygun olduğunda geçerlidir. POST isteği önbelleğe almayı etkinleştirmek için Hello alınabilir HTTP yöntemleri özelliğini kullanın.
- Merhaba istek gövdesi için dikkate alınır:
    - x-www-form-urlencoded değerleri
    - Benzersiz bir önbellek anahtar sağlama
- Büyük en fazla istek gövdesi boyutu tanımlama veri teslim performansını etkileyebilir.
    - **Önerilen değer:** 14 Kb
    - **Minimum değer:** 1 Kb

**Varsayılan davranış:** 14 Kb
 
## <a name="url"></a>URL

Bu özellikler bir istek toobe izin yeniden yönlendirilen veya tooa farklı bir URL'ye yeniden yazılmıştır.

Ad | Amaç
-----|--------
Yeniden yönlendirmeleri izleyin | İstekleri bir müşteri kaynak sunucu tarafından döndürülen hello konum üstbilgisi tanımlanan yeniden yönlendirilen toohello ana bilgisayar adı izin verilip verilmeyeceğini belirler.
URL yeniden yönlendirme | Merhaba konum üstbilgisi keşfi yönlendirir.
URL yeniden yazma  | Merhaba istek URL'si yeniden yazar.

###<a name="follow-redirects"></a>Yeniden yönlendirmeleri izleyin
**Amaç:** istekleri müşteri kaynak sunucu tarafından döndürülen konum üstbilgisi tanımlanan yeniden yönlendirilen toohello ana bilgisayar adı izin verilip verilmeyeceğini belirler.

Anahtar bilgileri:

- İstekler yalnızca toohello karşılık gelen yeniden yönlendirilen tooedge CNAME'ler olması aynı platformu.

Değer|Sonuç
-|-
Etkin|İstekler yönlendirilebilir.
Devre dışı|İstekleri yönlendirilir değil.

**Varsayılan davranış:** devre dışı bırakılmış.
###<a name="url-redirect"></a>URL yeniden yönlendirme
**Amaç:** istekleri konum üstbilgisi aracılığıyla yeniden yönlendirir.

Bu özelliğin Hello yapılandırma seçenekleri aşağıdaki hello ayarlanması aşağıdakileri gerektirir:

Seçenek|Açıklama
-|-
Kod|Toohello isteyenin döndürülecek hello yanıt kodu seçin.
Kaynak & düzeni| Bu ayarları yeniden yönlendirilen istekleri hello türünü tanımlayan bir istek URI düzeni tanımlayın. Yalnızca istek URL'si ölçütleri aşağıdaki hello her ikisi de karşılayan yönlendirilir: <br/> <br/> **Kaynak:** (veya içerik erişim noktası) bir kaynak sunucuyu tanımlar göreli bir yol seçin. Merhaba "/XXXX/" bölümü ve uç nokta adınız budur. <br/> **Kaynak (desen):** göreli yolu tarafından istekleri tanımlayan bir desen tanımlanması gerekir. Bu normal ifade deseni hello daha önce içerik erişim noktası (yukarıya bakın) seçtikten sonra başlayan doğrudan bir yol tanımlamanız gerekir. <br/> -Emin olun yukarıda tanımlanan hello istek URI ölçütleri (yani, kaynak & düzeni) çakışmadığını bu özellik için tanımlı hiçbir eşleşme koşullarla. <br/> -Bir desen toospecify emin olun. Merhaba deseni olarak boş bir değer kullanarak hello seçilen kaynak sunucuyu (örn., http://cdn.mydomain.com/) istekleri toohello kök klasörüne yalnızca eşleşir.
Hedef| Merhaba URL tanımlamak toowhich hello istekleri yukarıda yönlendirilirsiniz. <br/> Dinamik olarak bu URL'yi kullanarak oluşturun: <br/> -Bir normal ifade deseni <br/>-HTTP değişkenleri <br/> Yedek hello kaynak desende kullanarak $ hello hedef modele yakalanmış hello değerleri _n_  nerede  _n_  onu yakalanan hello sıraya göre bir değer tanımlar. Örneğin, $1 $2 hello ikinci değer temsil ederken hello kaynak desende yakalanan hello ilk değerini temsil eder. <br/> 
Yüksek oranda olan mutlak bir URL toouse önerilir. göreli bir URL Hello kullanımını CDN URL'leri tooan geçersiz yola yönlendirme.

**Örnek senaryo**

Bu örnekte, biz nasıl tooredirect toothis çözümler CNAME URL kenar temel CDN URL'sine gösterilmektedir: http://marketing.azureedge.net/brochures

Uygun istekleri olacaktır yeniden yönlendirilen toothis temel kenar CNAME URL: http://cdn.mydomain.com/resources

Bu URL yeniden yönlendirme yapılandırması aşağıdaki hello elde edilebilir:![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**Önemli noktaları:**

- Merhaba URL'sini yeniden yönlendirme özelliğini tanımlar hello yönlendirilir ve URL'leri isteği. Sonuç olarak, ek eşleme koşulları gerekli değildir. Yalnızca "her zaman" Merhaba eşleşme koşul tanımlandı ancak bu noktası toohello "Merhaba"Pazarlama"Müşteri kaynağındaki klasör yönlendirilecek broşürler" ister. 
- Eşleşen tüm istekleri hedef seçeneğinde CNAME URL tanımlanan yeniden yönlendirilen toohello kenar olacaktır. 
    - Örnek Senaryo #1: 
        - Örnek istek (CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf 
        - (Sonra yeniden yönlendirme) istek URL'si: http://cdn.mydomain.com/resources/widgets.pdf  
    - Örnek Senaryo #2: 
        - Örnek istek (Kenar CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf 
        - (Sonra yeniden yönlendirme) istek URL'si: http://cdn.mydomain.com/resources/widgets.pdf örnek senaryosu
    - Örnek Senaryo #3: 
        - Örnek istek (Kenar CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - (Sonra yeniden yönlendirme) istek URL'si: http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- Merhaba istek düzeni (% {Şeması}) değişken hedef seçeneğinde de. Bu, o hello isteğin düzenini yeniden yönlendirmeden sonra değişmeden kalır sağlar.
- Yeni bir URL'ye eklenen toohello "$1." aracılığıyla hello isteğinden yakalanan hello URL kesimleri olan
 
###<a name="url-rewrite"></a>URL yeniden yazma
**Amaç:** hello istek URL'si yeniden yazar.

Anahtar bilgileri:

- Bu özelliğin Hello yapılandırma seçenekleri aşağıdaki hello ayarlanması aşağıdakileri gerektirir:

Seçenek|Açıklama
-|-
 Kaynak & düzeni | Bu ayarları yeniden yazılmıştır istekleri hello türünü tanımlayan bir istek URI düzeni tanımlayın. Yalnızca istek URL'si ölçütleri aşağıdaki hello her ikisi de karşılayan yazılacaktır: <br/>     - **Kaynak (veya içerik erişim noktası):** bir kaynak sunucuyu tanımlar göreli bir yol seçin. Merhaba "/XXXX/" bölümü ve uç nokta adınız budur. <br/> - **Kaynak (desen):** göreli yolu tarafından istekleri tanımlayan bir desen tanımlanması gerekir. Bu normal ifade deseni hello daha önce içerik erişim noktası (yukarıya bakın) seçtikten sonra başlayan doğrudan bir yol tanımlamanız gerekir. <br/> Yukarıda tanımlanan hello istek URI ölçütleri (yani, kaynak & düzeni) çakışmadığını, bu özellik için tanımlanan hello eşleşme koşullardan herhangi biri ile emin olun. Bir desen toospecify emin olun. Merhaba deseni olarak boş bir değer kullanarak hello seçilen kaynak sunucuyu (örn., http://cdn.mydomain.com/) istekleri toohello kök klasörüne yalnızca eşleşir. 
 Hedef  |Merhaba göreli URL tanımlamak toowhich hello istekleri yukarıda yeniden yazılmıştır tarafından: <br/>    1. Kaynak sunucu tanımlayan bir içerik erişim noktası seçme. <br/>    2. Göreli yolu kullanarak tanımlama: <br/>        -Bir normal ifade deseni <br/>        -HTTP değişkenleri <br/> <br/> Yedek hello kaynak desende kullanarak $ hello hedef modele yakalanmış hello değerleri _n_  nerede  _n_  onu yakalanan hello sıraya göre bir değer tanımlar. Örneğin, $1 $2 hello ikinci değer temsil ederken hello kaynak desende yakalanan hello ilk değerini temsil eder. 
 Bu özellik, geleneksel bir yeniden yönlendirme yapmadan toorewrite hello URL kenar sunucularımızda sağlar. Başka bir deyişle, bu hello talep sahibinin aynı yanıt kodu yeniden yazılmıştır hello URL istenen sanki hello alırsınız.

**Örnek Senaryo 1**

Bu örnekte, biz nasıl tooredirect toothis çözümler CNAME URL kenar temel CDN URL'sine gösterilmektedir: http://marketing.azureedge.net/brochures/

Uygun istekleri olacaktır yeniden yönlendirilen toothis temel kenar CNAME URL: http://MyOrigin.azureedge.net/resources/

Bu URL yeniden yönlendirme yapılandırması aşağıdaki hello elde edilebilir:![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**Örnek Senaryo 2**

Bu örnekte, biz gösterilmektedir nasıl tooredirect normal ifadeler kullanarak büyük toolowercase bir kenarından CNAME URL.

Bu URL yeniden yönlendirme yapılandırması aşağıdaki hello elde edilebilir:![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**Önemli noktaları:**

- Merhaba URL yeniden yazma özelliği tanımlar hello yazılacak URL'leri isteyin. Sonuç olarak, ek eşleme koşulları gerekli değildir. Yalnızca "her zaman" Merhaba eşleşme koşul tanımlandı ancak bu noktası toohello "Merhaba"Pazarlama"Müşteri kaynak klasörü yazılacak broşürler" ister.

- Yeni bir URL'ye eklenen toohello "$1." aracılığıyla hello isteğinden yakalanan hello URL kesimleri olan



###<a name="compatibility"></a>Uyumluluk

Bu özellik, uygulanan tooa isteği olabilir önce karşılanması gereken ölçütlerle eşleşen içerir. Sipariş tooprevent ayarında çakışan eşleştirme ölçütü, bu özellik eşleşme koşullar aşağıdaki hello ile uyumlu değil:

- Sayı olarak
- CDN kaynak
- İstemci IP adresi
- Müşteri kaynağı
- İstek düzeni
- URL yolu dizini
- URL yolu genişletme
- URL yolu dosya
- URL yolu değişmez değeri
- URL yolu Regex
- URL yolu joker karakter
- URL sorgu değişmez değeri
- URL sorgu parametresi
- URL sorgu Regex
- URL sorgu joker karakter


## <a name="next-steps"></a>Sonraki Adımlar
* [Kuralları altyapısı başvurusu](cdn-rules-engine-reference.md)
* [Kurallar altyapısı koşullu ifadeler](cdn-rules-engine-reference-conditional-expressions.md)
* [Kurallar altyapısı eşleşme koşulları](cdn-rules-engine-reference-match-conditions.md)
* [Merhaba kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma](cdn-rules-engine.md)
* [Azure CDN'ye genel bakış](cdn-overview.md)
