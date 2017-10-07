---
title: "aaaAzure geçişi karma bağlantılar protokol Kılavuzu | Microsoft Docs"
description: "Azure geçişi karma bağlantılar Protokolü Kılavuzu."
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Azure geçişi karma bağlantılar Protokolü
Azure geçiş hello anahtar özelliği ayaklar hello Azure Service Bus platformun biridir. Merhaba yeni *karma bağlantılar* yetenektir geçişinin HTTP ve WebSockets dayalı bir güvenli, açık Protokolü evrimi. Eşit oranda adlı hello eski yerini *BizTalk Services* özel Protokolü foundation üzerinde oluşturulmuş özellik. Merhaba tümleştirmeye karma bağlantılar, Azure App Services toofunction olarak devam edecek-değil.

Karma bağlantılar sırasında birini veya her ikisini tarafların NAT veya güvenlik duvarı arkasında bulunduğu iki ağa bağlı uygulamalar arasında çift yönlü, ikili akış iletişim sağlar. Bu makalede bağlanan istemciler dinleyicisi ve gönderen rol ve nasıl dinleyicileri yeni bağlantıları kabul etmek için hello karma bağlantılar geçiş ile Merhaba istemci tarafı etkileşimler açıklanmaktadır.

## Etkileşim modeli
Merhaba karma bağlantılar geçiş hello Azure bulut, hem tarafların bulmak ve kendi ağın perspektif toofrom bağlanmak randevu noktasında sağlayarak iki taraf bağlanır. Bu randevu noktası "karma" Bu ve diğer belgelerin hello API'leri hem de Azure portal hello bağlantısıdır. Merhaba karma hizmet uç noktası bağlantıları tooas hello "hizmet" hello, bu makalenin kalanında için denir. diğer ağ birçok API'ler tarafından kurulan hello terminolojisi üzerinde Hello etkileşim modeli leans.

İlk hazırlık toohandle gelen bağlantıları gösterir ve daha sonra bunları kabul geldikçe dinleyici yoktur. Üzerindeki diğer taraftaki Merhaba, hello dinleyicisi, çift yönlü iletişim yolu kurmak için kabul o bağlantı toobe bekleniyor doğrultusunda bağlayan bağlanan bir istemcinin yoktur.
"Bağlan", "Dinleme," ve "Kabul" olan hello aynı çoğunda bulun terimler yuva API'leri.

Herhangi bir geçişli iletişim modelini hello "dinleyicisi", "istemci" de cümlecik kullanımda hale getirir. ve diğer terminolojisi aşırı da neden olabilir bir hizmet uç noktası doğru giden bağlantı her iki taraf sahiptir. Bu nedenle karma bağlantılar için kullandığımız hello kesin terminolojisi aşağıdaki gibidir:

istemcileri toohello hizmet olduğundan bağlantısının her iki tarafında hello programlar "istemcileri," adı verilir. Merhaba bekler ve bağlantıları "dinleyicisi" ya da kabul eden istemci denirse toobe rolündeki hello"dinleyicisi." hello hizmeti üzerinden bir dinleyici doğru yeni bir bağlantı başlatır hello istemci hello "gönderen" adlı ya da "gönderen rol."

### Dinleyici etkileşimleri
Merhaba dinleyicisi hello hizmetiyle dört etkileşimleri; yine de sahip istiyor musunuz? Tüm kablo ayrıntıları hello başvuru bölümünde bu makalenin sonraki bölümlerinde açıklanmıştır.

#### Dinleme
tooindicate hazırlık toohello hizmet dinleyici hazır tooaccept bağlantıları olduğundan, bir giden WebSocket bağlantısı oluşturur. Merhaba bağlantı el sıkışması hello geçiş ad alanı ve bu ad hello "Dinleme" hakkı confers bir güvenlik belirteci yapılandırılmış karma bağlantı hello adını taşır.
Merhaba WebSocket hello hizmeti tarafından kabul edildiğinde hello kayıt tamamlandıktan ve web WebSocket hello "etkinleştirilmesine yönelik tüm sonraki etkileşimler denetim kanalı" olarak Canlı tutulur hello kurulmuş. Karma bir bağlantı üzerindeki too25 eşzamanlı dinleyicileri yukarı Hello hizmet verir. İki veya daha fazla etkin dinleyiciler varsa, gelen bağlantıları bunları rastgele sırayla dengeli; Orta dağıtım garanti edilmez.

#### Kabul et
Bir gönderici hello hizmet üzerinde yeni bir bağlantı açıldığında hello hizmet seçer ve hello etkin dinleyicileri hello karma bağlantı üzerinde birini bildirir. Bu bildirim toohello dinleyicisi dinleyicisi hello hello WebSocket bitiş noktası içeren hello URL'sini hello bağlantı kabul toofor bağlanmalısınız JSON ileti olarak hello açık denetim kanalı üzerinden gönderilir.

Merhaba URL olabilir ve doğrudan ek iş olmadan hello dinleyicisi tarafından kullanılan gerekir.
Kodlanmış hello bilgileri yalnızca istekli toowait hello bağlantı kurulan toobe uçtan uca, ancak tooa en çok 30 saniyelik yukarı hello gönderen olarak zaman, aslında sürece kısa bir süre için geçerlidir. Merhaba URL yalnızca bir başarılı bağlantı denemesinde için kullanılabilir. Kısa sürede hello gelen URL kurulduğunda, hello randevu bu WebSocket tüm başka faaliyete bağlantıyla geçişli WebSocket ve herhangi bir araya veya hello hizmeti tarafından tercüme olmadan toohello gönderen.

#### Yenile
Merhaba dinleyicisi etkinken denetim kanalı sona erebilir korumak ve kullanılan tooregister hello dinleyicisi olmalıdır hello güvenlik belirteci. Merhaba belirteç süre sonu devam eden bağlantılarını etkilemez, ancak hello hizmet düzeyinde veya sona erme hello anda hemen sonra tarafından bırakılan hello denetim kanalı toobe neden olmaz. Merhaba "Yenile" Merhaba denetim kanalı için uzun süreler sürdürülebilir şekilde dinleyicisi hello bir JSON ileti hello denetim kanalı ile ilişkili tooreplace hello belirteci gönderebilirsiniz işlemdir.

#### Ping
Merhaba denetim kanalı aracılar hello şekilde üzerinde uzun bir süre için boşta kalırsa gibi yük Dengeleyiciler ya da NAT hello TCP bağlantısı kaybolmasına neden olabilir. Merhaba "ping" işlemi toobe Canlı tasarlanmıştır, çok küçük miktarda veri herkes hello ağdaki yönlendiricilerin anımsatır hello kanalda bu hello bağlantı göndererek önler ve dosyayı hello dinleyicisinin "canlı" test olarak sunar. Merhaba ping başarısız olursa, hello denetim kanalı kullanılamaz olarak düşünülmelidir ve hello dinleyiciyi yeniden bağlanmanız.

### Gönderen etkileşimi
Hello göndericisi yalnızca tek bir etkileşim hello hizmetiyle vardır: bağladığı.

#### Bağlan
Merhaba "Bağlan" işlemi WebSocket hello hizmet sağlayan hello adı hello karma bağlantı ve (isteğe bağlı olarak, ancak gerekli varsayılan olarak) üzerinde "Gönderme" izni hello sorgu dizesinde conferring bir güvenlik belirteci açar. Hello hizmet şekilde daha önce açıklanan hello hello dinleyicisinde etkileşim ve bu WebSocket ile birleştirilmiş bir randevu bağlantı hello dinleyicisi oluşturur. Merhaba WebSocket kabul ettikten sonra bu WebSocket üzerinde tüm diğer etkileşimler ile bağlantılı bir dinleyici ' dir.

### Etkileşim özeti
Merhaba Bu etkileşim model hello gönderen istemci el sıkışması "temiz" WebSocket bağlı tooa dinleyicisi olduğu ve herhangi bir başka preambles veya hazırlama gereken ile dışında gelir sonucudur. Bu model, kendi WebSocket istemci katmana doğru şekilde oluşturulmuş bir URL sağlayarak neredeyse her varolan WebSocket istemci uygulaması tooreadily faydalanan hello karma bağlantılar hizmeti sağlar.

Dinleyici hello WebSocket kabul etkileşim edinir hello randevu bağlantı da temiz ve tooany varolan WebSocket sunucu uygulamasıyla "arasında kabul et" ayırt bazı en az bir ek Özet karmalayan kendi framework'ün yerel ağ dinleyicileri ve karma bağlantılar uzak işlemler "işlemleri kabul".

## Protokolü başvurusu

Bu bölümde daha önce açıklanan hello Protokolü etkileşimlerin hello Ayrıntılar açıklanmaktadır.

Tüm WebSocket bağlantılar bağlantı noktası 443 üzerinde bazı WebSocket framework veya API tarafından yaygın olarak soyutlanır HTTPS 1.1'den yükseltme olarak yapılır. Açıklamayı buraya uygulama belirli bir framework öneren olmadan nötr, tutulur.

### Dinleyici Protokolü
Merhaba dinleyici Protokolü iki bağlantı hareketleri ve üç ileti işlemlerini oluşur.

#### Dinleyici denetim kanalı bağlantısı
Merhaba denetim kanalı WebSocket bağlantı oluşturma konusunda açıldığında:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

Merhaba `namespace-address` hello Azure geçiş ad alanı konakları hello formunun genellikle karma bağlantı hello hello tam etki alanı adı `{myname}.servicebus.windows.net`.

Merhaba sorgu dizesi parametresi seçenekleri aşağıdaki gibidir.

| Parametre | Gerekli | Açıklama |
| --- | --- | --- |
| `sb-hc-action` |Evet |Merhaba dinleyicisi rol Merhaba parametresi olmalıdır **sb hc eylem dinleme =** |
| `{path}` |Evet |Merhaba Hello URL kodlanmış ad alanı yolu karma bağlantı tooregister bu dinleyici üzerinde önceden yapılandırılmış. Sabit eklenmiş toohello bu ifadesidir `$hc/` yol bölümü. |
| `sb-hc-token` |Evet\* |Merhaba dinleyicisi bir geçerli, URL kodlanmış Service Bus paylaşılan erişim belirteci hello ad alanı veya hello confers karma bağlantı için sağlamalıdır **dinleme** doğru. |
| `sb-hc-id` |Hayır |Bu istemci tarafından sağlanan isteğe bağlı kimliği uçtan uca Tanılama izleme sağlar. |

Merhaba WebSocket bağlantısı kaydedilmemiş, toohello karma bağlantı yolu veya eksik veya geçersiz bir belirteç veya başka bir hata başarısız olursa, hello hata geri bildirim hello normal HTTP 1.1 durumu geri bildirim modeli kullanılarak sağlanır. Durum açıklaması bir hata izleme-Azure destek personeli için iletilen kimliğini içerir:

| Kod | Hata | Açıklama |
| --- | --- | --- |
| 404 |Bulunamadı |Merhaba karma bağlantı yolu geçersiz veya hello temel URL biçimi yanlış. |
| 401 |Yetkilendirilmemiş |Merhaba güvenlik belirteci eksik veya hatalı biçimlendirilmiş veya geçersiz olur. |
| 403 |Yasak |Merhaba güvenlik belirteci, bu eylem için bu yol için geçerli değil. |
| 500 |İç hata |Bir hello hizmetinde sorun oluştu. |

Başlangıçta yukarı, bir izleme de içeren açıklayıcı bir hata iletisi ile birlikte uygun WebSocket protokolü hata kodu kullanarak iletilen böylece hello nedeni ayarlandı sonra hello WebSocket bağlantısı bilerek hello hizmeti tarafından kapatılırsa KİMLİĞİ. Merhaba hizmet denetim kanalı bir hata koşulu karşılaşılmadan kapanır değil. Temiz bir kapatma denetlenen istemcidir.

| WS durumu | Açıklama |
| --- | --- |
| 1001 |Merhaba karma bağlantı yolu silinmiş veya devre dışı. |
| 1008 |Merhaba güvenlik belirtecinin süresi doldu, bu nedenle hello yetkilendirme ilkesini ihlal etti. |
| 1011 |Bir hello hizmetinde sorun oluştu. |

### Anlaşma kabul et
Merhaba "kabul" bildirim, JSON ileti WebSocket metin çerçevesinde olarak, daha önce oluşturulmuş denetim kanalı üzerinden hello hizmet toohello dinleyicisi tarafından gönderilir. Hiçbir yanıt toothis iletisi yok.

Merhaba ileti şu anda aşağıdaki özelliklere hello tanımlayan "kabul et" adlı bir JSON nesnesi içerir:

* **Adres** – hello WebSocket toothe hizmet tooaccept gelen bağlantı kurmak için kullanılan URL dizesi toobe hello.
* **Kimliği** – Bu bağlantı için benzersiz tanımlayıcı hello. Hello kimliği hello gönderen istemci tarafından sağlanan, onu hello sağlanan gönderen değeri, aksi takdirde, sistem tarafından oluşturulan değer.
* **connectHeaders** – kaldırılmış tüm HTTP üstbilgilerin toohello geçiş endpoint hello sn WebSocket protokolü ve sn WebSocket uzantıları üstbilgileri de içeren hello gönderen tarafından sağlanan.

#### İleti kabul et

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

Başlangıç adresi URL hello JSON ileti hello dinleyicisi tarafından kurmak için kullanılan sağlanan hello WebSocket kabul etme veya reddetme hello gönderen yuva için.

#### Merhaba Yuva kabul etme
tooaccept, WebSocket bağlantı sağlanan toohello adresi hello dinleyicisi oluşturur.

Merhaba, "kabul" izleme iletisi bir `Sec-WebSocket-Protocol` üstbilgisi, o hello dinleyicisi bu Protokolü'nü destekliyorsa hello WebSocket yalnızca kabul beklenir. Ayrıca, WebSocket kurulan hello hello üstbilgisini ayarlar.

Merhaba aynı toohello geçerlidir `Sec-WebSocket-Extensions` üstbilgi. Merhaba framework uzantı destekliyorsa, hello üstbilgi toohello sunucu tarafı yanıt gerekli Merhaba, ayarlamalısınız `Sec-WebSocket-Extensions` el sıkışma hello uzantısı.

Merhaba URL kullanılan, olarak-hello kurmak için olan Yuva kabul eder, ancak aşağıdaki parametreleri içerir:

| Parametre | Gerekli | Açıklama |
| --- | --- | --- |
| `sb-hc-action` |Evet |Bir yuva kabul etmek için hello parametresi olmalıdır`sb-hc-action=accept` |
| `{path}` |Evet |(paragraf aşağıdaki hello bakın) |
| `sb-hc-id` |Hayır |Önceki açıklamasına bakın **kimliği**. |

`{path}`hello Hello URL kodlanmış ad alanı yolu hangi tooregister karma bağlantı, bu dinleyiciyi önceden yapılandırılmış olur. Sabit eklenmiş toothe bu ifadesidir `$hc/` yol bölümü. 

Merhaba `path` ifade genişletilmiş bir sonek ve ayıran eğik sonra hello kayıtlı adından sonra bir sorgu dizesi ifadesi. Bu, olası tooinclude HTTP üstbilgileri değilse hello gönderen istemci toopass gönderme bağımsız değişkenleri toohello kabul dinleyicisi sağlar. Merhaba Beklenti bu hello dinleyicisi framework ayrıştırır hello sabit yol bölümü ve yolundan hello kayıtlı adı olduğundan ve hello kalan büyük olasılıkla önüne hiçbir sorgu dizesi bağımsız değişkenler olmadan yapar `sb-`, kullanılabilir toohello uygulama karar tooaccept bağlantı hello olup olmadığını.

Daha fazla bilgi için "Gönderen Protokolü" bölümünde aşağıdaki hello bakın.

Varsa bir hata, hello hizmeti gibi yanıtlayabilir:

| Kod | Hata | Açıklama |
| --- | --- | --- |
| 403 |Yasak |Merhaba URL geçerli değil. |
| 500 |İç hata |Bir hello hizmetinde sorun oluştu |

Merhaba bağlantı kurulduktan sonra hello gönderen WebSocket aşağı ya da durum aşağıdaki hello ile kapattığında hello sunucu WebSocket hello kapatır:

| WS durumu | Açıklama |
| --- | --- |
| 1001 |Merhaba gönderen istemci hello bağlantıyı kapatır. |
| 1001 |Merhaba karma bağlantı yolu silinmiş veya devre dışı. |
| 1008 |Merhaba güvenlik belirtecinin süresi doldu, bu nedenle hello yetkilendirme ilkesini ihlal etti. |
| 1011 |Bir hello hizmetinde sorun oluştu. |

#### Merhaba yuva reddetme
Merhaba durum kodu ve durum açıklaması hello reddetme nedeni akabilir iletişim toohello gönderen yedekleme benzer bir el sıkışması "kabul" İnceleme selamlama iletisine gerektirir sonra hello yuva reddetme.

Böylece dinleyicisi istemci uygulamaları toorely WebSocket istemcide devam edebilirsiniz ve gerekmez fazladan kullandığınızda, HTTP istemci tam hello Protokolü tasarım burada toouse (yani tanımlanmış hata durumuna tasarlanmış tooend) bir Web yuvası anlaşması seçimdir.

tooreject hello yuva hello istemci selamlama iletisine "kabul" Merhaba adresinden URI alır ve iki sorgu dizesi parametreleri tooit, aşağıdaki gibi ekler:

| Param | Gerekli | Açıklama |
| --- | --- | --- |
| statusCode |Evet |Sayısal HTTP durum kodu. |
| StatusDescription |Evet |Merhaba reddetme İnsan okunabilir açıklaması. |

Sonuçta elde edilen URI ise hello tooestablish WebSocket bağlantısı kullanılır.

Hiçbir WebSocket kurulduktan sonra doğru tamamlarken, bu el sıkışma bilerek 410, HTTP hata koduyla başarısız olur. Bir sorun yaşanırsa hello hata kodları aşağıdaki hello açıklanmaktadır:

| Kod | Hata | Açıklama |
| --- | --- | --- |
| 403 |Yasak |Merhaba URL geçerli değil. |
| 500 |İç hata |Bir hello hizmetinde sorun oluştu. |

### Dinleyici belirteci yenileme
Merhaba dinleyicisi belirteci hakkında tooexpire olduğunda, bir metin çerçeve ileti toohello hizmeti oluşturulmuş hello denetim kanalı aracılığıyla göndererek değiştirebilirsiniz. İleti adlı bir JSON nesnesi içerir `renewToken`, özelliği şu anda aşağıdaki hello tanımlar:

* **belirteç** – ad alanı veya hello confers karma bağlantı için geçerli, URL kodlanmış bir hizmet veri yolu paylaşılan erişim belirteci **dinleme** doğru.

#### renewToken iletisi

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

Merhaba belirteci doğrulama başarısız olursa, erişim reddedildi ve hello bulut hizmeti bir hata ile Merhaba denetim kanalı WebSocket kapatır. Aksi durumda yanıt yoktur.

| WS durumu | Açıklama |
| --- | --- |
| 1008 |Merhaba güvenlik belirtecinin süresi doldu, bu nedenle hello yetkilendirme ilkesini ihlal etti. |

## Gönderen Protokolü
Merhaba gönderen Protokolü dinleyici kurulan etkili bir şekilde aynı toohello yoludur.
Merhaba hedeftir hello uçtan uca için maksimum saydamlığı WebSocket. Merhaba adresi toois hello hello dinleyicisi ancak hello "eylem" aynıdır farklıdır ve belirteç bağlanmak için farklı bir izin gerekir:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

Merhaba *ad alanı adresi* hello Azure geçiş ad alanı konakları hello formunun genellikle karma bağlantı hello hello tam etki alanı adı `{myname}.servicebus.windows.net`.

Merhaba isteği uygulama tanımlı olanlar da dahil olmak üzere, rasgele ek HTTP üstbilgileri içerebilir. Tüm üstbilgiler akış toohello dinleyicisi tarafından sağlanan ve hello üzerinde bulunabilir `connectHeader` hello nesnesinin **kabul** denetim iletisi.

Merhaba sorgu dizesi parametresi seçenekleri aşağıdaki gibidir:

| Param | Gerekli mi? | Açıklama |
| --- | --- | --- |
| `sb-hc-action` |Evet |Merhaba gönderen rolü için hello parametresi olmalıdır `action=connect`. |
| `{path}` |Evet |(paragraf aşağıdaki hello bakın) |
| `sb-hc-token` |Evet\* |Merhaba dinleyicisi bir geçerli, URL kodlanmış Service Bus paylaşılan erişim belirteci hello ad alanı veya hello confers karma bağlantı için sağlamalıdır **Gönder** doğru. |
| `sb-hc-id` |Hayır |Uçtan uca Tanılama izleme sağlar ve kullanılabilir toohello dinleyicisi hello sırasında yapılan bir isteğe bağlı kimlik el sıkışma kabul edin. |

Merhaba `{path}` olan hello hello URL kodlanmış ad alanı yolu önceden yapılandırılmış hangi tooregister karma bağlantıda bu dinleyicisi. Merhaba `path` ifadesi uzatabilirsiniz sonek ve başka bir sorgu dizesi ifade toocommunicate. Merhaba karma bağlantı hello yolu altında kaydedilmişse `hyco`, hello `path` ifade olabilir `hyco/suffix?param=value&...` hello sorgu dizesi parametreleri burada tanımlanan tarafından izlenen. Tam bir deyim aşağıdaki gibi olabilir:

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

Merhaba `path` ifade toohello dinleyicisi hello adresindeki hello "kabul" denetimi iletisinde bulunan URI üzerinden geçirilir.

Merhaba WebSocket bağlantısı toohello karma bağlantı yolu olmayan Kaydedilmekte, eksik veya geçersiz bir belirteç veya başka bir hata başarısız olursa, hello hata geri bildirim hello normal HTTP 1.1 durumu geri bildirim modeli kullanılarak sağlanır. Durum açıklaması izleme bildirilmesi kimliği Azure destek personeli için bir hata içeriyor:

| Kod | Hata | Açıklama |
| --- | --- | --- |
| 404 |Bulunamadı |Merhaba karma bağlantı yolu geçersiz veya hello temel URL biçimi yanlış. |
| 401 |Yetkilendirilmemiş |Merhaba güvenlik belirteci eksik veya hatalı biçimlendirilmiş veya geçersiz olur. |
| 403 |Yasak |Merhaba güvenlik belirteci bu yol için ve bu eylem için geçerli değil. |
| 500 |İç hata |Bir hello hizmetinde sorun oluştu. |

Merhaba WebSocket bağlantısı bilerek, başlangıçta ayarlandığına sonra hello hizmeti tarafından kapatılırsa, hello nedeni bu nedenle de içeren açıklayıcı bir hata iletisi ile birlikte uygun WebSocket protokolü hata kodu kullanarak iletilen bir İzleme kimliği.

| WS durumu | Açıklama |
| --- | --- |
| 1000 |Merhaba dinleyicisi hello yuva kapatın. |
| 1001 |Merhaba karma bağlantı yolu silinmiş veya devre dışı. |
| 1008 |Merhaba güvenlik belirtecinin süresi doldu, bu nedenle hello yetkilendirme ilkesini ihlal etti. |
| 1011 |Bir hello hizmetinde sorun oluştu. |

## Sonraki adımlar
* [Geçiş hakkında SSS](relay-faq.md)
* [Ad alanı oluşturma](relay-create-namespace-portal.md)
* [.NET kullanmaya başlama](relay-hybrid-connections-dotnet-get-started.md)
* [Node kullanmaya başlama](relay-hybrid-connections-node-get-started.md)

