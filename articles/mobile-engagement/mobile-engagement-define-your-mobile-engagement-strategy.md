---
title: aaaDefine Mobile Engagement stratejinizi | Microsoft Docs
description: "Bilgi nasıl tooonboard ve analizler ve anında iletme bildirimleri ile Mobile Engagement en iyi duruma getirme."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7533e318-81b9-4360-aace-b7be8225985b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: afe32cb71019092eb28f2a8557404d60ad48ada4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="define-your-mobile-engagement-strategy"></a>Mobile Engagement stratejinizi tanımlama
*Uygulamanızı bir nedenle yazdınız: toohave kullanıcılarınızın bunu kullanın!*

İnanıyoruz kesinlikle put mükemmel baş toomake çalışılırken çaba, kullanıcıların hayran kalacağı harika bir uygulama. Ayrıca muhtemelen bir oldukça büyük pazarlama bütçe tooacquire kullanıcıların yatırımı. Ancak hello ilk heyecan verici dönemin ardından kullanıcıların, sonra bunları uygulamanızı kullanan yavaş Dur görebilirsiniz. *Bu Azure Mobile Engagement İşte!* : toostick dolaşma ve tooincrementally izin uygulamanız test edip öğrenme.

Bizim yaklaşım tooimproving tutma ve kullanım uygulaması kullanıcılara anında iletme bildirimleri ve uygulama içi iletiler aracılığıyla, ancak iletiler ve iletişim, toothem, uygulamanızdaki her according tootheir davranışa çok özel bir şekilde çekici dayanır. Amacımız hello doğru zamanı ve hello doğru konuma hello doğru hedef kitleye ile iletişim toolet ' dir.

Ancak bunun için toostart ile gerekir *kullanıcılarınızı anlamakla*, ardından, yaptıklarına veya özelliklerine (bunlara Segment diyoruz) temel alan gruplar ve ardından ilgili iletişimler tooeach segment oluşturun.

## <a name="mobile-engagement-serves-your-objectives"></a>Mobile Engagement hedeflerinize hizmet eder
*Elde tutma ve kullanım hakkında konuştuk, ancak amacımız nedir?*

Mobile Engagement stratejinizi oluştururken önce uygulamanızın hedeflerine ve ana performans göstergelerine (KPI) bakmak gerekir.

Merhaba hedeflerine ve toodefine, katılım sağlayan kullanım örneklerinizi doğru bakış açısından hello ile Yardım KPI'leri tanımlayarak başlatın.

Kullanım örnekleri, BT sisteminiz tarafından tetiklenen yardımcı program bildirimine toomake toocommunicate hello basit bir karşılamadan, toohello çok arasında değişen kullanıcılarınız Gelişmiş istediğinizi Kampanyalar basit bir listesi verilmiştir. İyi oluşturulmuş bir kullanım örneği en az içermelidir hello sorularının cevabını *what-kim-ne zaman*:

1. Çok kısa bir ad (örneğin bir "Hoş geldiniz kampanyası").
2. **Ne**: bir ileti örneği (örneğin, "memnun toohave, yerleşik! Toologin tooget unutmayın, 1 aylık ücretsiz! "). Bu iletiyi yok mümkün toochange olacak nihai yollarla, dilediğiniz zaman bağlıdır, ancak genellikle toosay istediğiniz toostart göz önünde bulundurulması hangi size yardımcı olur.
3. **Kimin**: (örneğin, "Merhaba uygulama hello için önce başlatılan tüm kullanıcılar 3 gün önce zaman, hello oturum açma sayfasını ziyaret etmiş ancak değil oturum açma") bu iletiyi alacak hello kesimi.
   * Evet, böyle bir şeyi Azure Mobile Engagement ile kolayca yapabilirsiniz :)
   * Bu yeniden toobe yok hello doğru verileri topladığınız segmentlerinizi istediğiniz zaman tanımlayabilirsiniz, ancak erken segment ölçütü tooensure üzerinde önemli toodefine olduğu gibi son.
4. **Zaman**: kampanyanızın zamanlaması hello. Belirli bir tarihte veya bir tetikleyiciye bağlı olarak belirli bir eylemden sonra olabilir. Mobile Engagement önemli bir olasılık toorightly zaman miktarı iletişimi sunar.

Kullanım örnekleri ve segmentin tanımlandıktan sonra bir uygulama içinde toplanması gereken bir kılavuz toodefine hello veri sağlar. Bu, hello rolüdür bir *"etiket planı"*. Bir etiket planı hello veri koleksiyonu, tooensure toohello geliştiriciler belirtilen sağlar. Bu nedenle, geliştiricilerin mümkün tooembed Mobile Engagement, hello önerilir, toowork kampanyalarınızın hello doğru verilerle sağ kurulumu. Aynı zamanda toorun testleri tooensure hello tümleştirmenin doğru olduğundan ve gerekenler toplar çok önemli olacaktır.

Bir Pazarlamacılar mümkün toosee analizlerinizi gerçek zamanlı, kitlenizi segmentlere ve olması toosend akıllı başlatmak gibi hello tümleştirmeye dayalı şekilde uygulamalar yayımlandıktan sonra son kullanıcılar ya da hello uygulama dışında anında iletme bildirimi tooengage hedeflenen.

### <a name="use-cases-tooget-started"></a>Kullanım örnekleri tooget başlatıldı
1. Hoş Geldiniz stratejisi: hello başlatma uygulamasının hello sırada D + 2/5/10/15 gün toore devreye hello ilk oturum ve artış ilk çalıştırma bekletme sonra hello son kullanıcı davranışına göre çeşitli anında iletme bildirimi kampanyaları oluşturun.
2. Merhaba son kullanıcı toosend hello bilgileri yalnızca tooend-büyük olasılıkla tooengage olan kullanıcıların Hello davranışını yeni içerik (özellik, makale/video veya ürün) yükseltirsiniz.
3. Merhaba uygulaması oranı: değerinden 1, en olası toorate hello uygulama 5 yıldız hello deposunda yüzdesi temel kullanıcı hedefleyin.
4. Abonelik artırma: bunları henüz görmemiş değerli içerikleri tooend-kullanıcılar tooincrease abonelik yükseltin.
5. Öğretici: Herkes için zorunlu öğreticilere son verin. Neden uygulama mükemmel öğreticiler ve daha sonra bunları yalnızca hello kullanıcı toonot kullanım görünüyorsa uygulama içi iletiler aracılığıyla uygulama hello veya bir özelliği kullanmakta zorluk çekiyorsa tetikleyicisi yapı?

## <a name="why-do-you-need-analytics-tooengage"></a>Neden analizi tooengage gerekiyor mu?
Bu noktada fark etmiş olabileceğiniz gibi yalnızca herkese giden bir anında iletme bildirimi kullanmak yeterli değildir. Merhaba temel kavramı, Mobile Engagement toohelp Pazarlamacılar ve geliştiricilerin hello doğru zamanda hello doğru son kullanıcıyla etkileşim ve hello sağ yerleştirin. tooknow bu üç ana kavramı temel toogather Analytics uygulamanızdan ve toosegment kullanın, İzleyici. Davranış segmentleri diğer veritabanınızdan veya CRM’den ya da çapraz bir kanaldan verilerle tamamlanırsa analiz daha da güç kazanır. Mobile Engagement yerden veri almaya olanak sağlar ve tootarget hello doğru hedef kitleye kullanır.

kitlenizi çekici zaman toobe hello en bağlamsal, onu mümkündür önemli toohave hello bilgi hello son kullanıcılar davranışının tooknow durumlarını gerçek zamanlı. Veri toplama, Pazarlamacılar toofocus gerçekten ne üzerine tooplay kullanım örnekleri önemlidir ve kendi mobil katılım strateji hedeflerine ulaşmasına olanak sağlar. Daha önce ayarlamak hello hedeflere ulaşmak olduğu da neden hello en iyi uygulama aslında değil toogather herhangi bir şey hello neden ve her şeyi hello analytics ancak yalnızca o toofocus izin hangi üzerinde toolearn ve kullanım örnekleri istiyor. Bu hello en iyi yolu toostart, deneyin, test ve nasıl anında iletme bildirimi toouse hello çözüm ve adres akıllı öğrenin ve bir uygulama toobring hello bekletme artırmak bu bir başarı öyküsü düzeyinde.

> [!NOTE]
> Unutmayın: Çok fazla veri hello veriye zarar verir!
> 
> 

### <a name="use-cases-and-best-practices"></a>Kullanım örnekleri ve en iyi yöntemler
Hello biz kısaca bazı ele alacağız aşağıdaki bölümlerde başlattığınız bizim müşteriler tooget karşılaştığımız gelen kullanım örnekleri anahtar.

#### <a name="media"></a>Medya
Merhaba hello son kullanıcı tarafından tüketilen içerik türünü toplayın ve ardından bu davranışı tootarget belirli türlerine göre daha büyük bir olasılıkla tooconsume olacaktır içerik yalnızca tooan İzleyici hello hedef kitlenizi segmentlere. Tüm kullanıcı tabanına istenmeyen posta gönderilmesini önler ve elde tutmayı artırır.

#### <a name="m-commerce"></a>M-ticaret
Merhaba ürün kategorileri içinde hello uygulama ve hedef kitle toopromote en sık ziyaret edilen indirim toplayabilir veya yeni ürün son kullanıcı hello bu kategorideki büyük olasılıkla toopurchase olacaktır. Tooboost gelirleri hedefleyin. Yeniden hello hedefi toospam değil!

#### <a name="gaming"></a>Oyun
Bir son kullanıcı ve başlangıç zamanı harcadığı hello oyundaki seviyesini toplamak kalmış olabilecek ve büyük olasılıkla toojump tooa sonraki bir ödül teklifini düzeyi olacaktır belirtilen dönem tootarget hello İzleyici.

Belirli olaylar hakkında bazı zaman tootry tooencourage için bunları tooreturn oynamamış bir no'lu tebliğ kapsamında teşvik toothose kullanıcılarla iletişim kurar.

#### <a name="retail"></a>Perakende
Merhaba ürünleri ya da bir hedef kitle Sık Kullanılanlar veya davranışı ve sürücü hello İzleyici tooyour deposu tooincrease satın alma gelirlerini göre daha büyük bir olasılıkla tooconsume olmalıdır markaları toplayın.

#### <a name="banking"></a>Bankacılık
Hello ilk hello uygulama başlatılırken bir hesap oluşturan son kullanıcılara verileri toplar. Toodeploy hedeflenen anında iletme bildirimi ile bir Hoş Geldiniz stratejisi hedeflenir ve hello hesap aboneliklerinin sayısını artırın.

### <a name="how-toocreate-a-great-tag-plan"></a>Nasıl toocreate harika bir etiket planı?
Bir etiket planı hello kullanıcı yolu veya yeterli analytics toounderstand kullanıcı davranışı ve düzgün şekilde segment hello kullanıcı temel toplanan toohave olması gereken tüm hello etiketleri (veri) sağlayan Merhaba uygulaması'nın iş akışı bir tür açıklamasını gibi olması gerekir. Bu teknik bir işlem değildir. Bu nedenle, Pazarlamacılar kendi Mobile Engagement stratejilerine göre toocollect istedikleri mümkün toospecify hello verilerdir.

Hello minimum tootag en az tüm hello ekranlar olduğu (adlı *etkinlikleri* Mobile Engagement içinde) bir uygulama. Bu, hello kullanıcı yolu belirlenmesine yardımcı olur.

Etkinlik, bir düğmeye tıklanması gibi eylem bilgilerini toplayan *olaylar* ekleyebilir. Bu hello uygulama içerisindeki etkileşimler toplanabilir hello koleksiyonunu sağlar. Bu nedenle, Pazarlamacılar sorgulayabilmesi tooknow hangi kullanıcıların ziyaret ve neler yaptıklarını verilmiştir.

`Jobs`süreli eylemlerdir. Bu kullanıcı toocreate için bir hesap veya toologin örneği için süreyi Pazarlamacılar toounderstand için çok kullanışlıdır. Bu ayrıca, bir web hizmeti toocall gereken süreyi geliştiriciler toomonitor için yararlı olabilir.

`Errors`Kullanıcıların uygulamanızda sorunlar yaşıyorsanız, izlenen tooknow de olabilir. Örneğin, sık sık bağlantı sorunlarıyla karşılaşılması.

Bu tür verilerin tümü parametrelerle Genişletilebilir (*ek bilgiler* Mobile Engagement içinde) hello uygulamadan dinamik veri toogather izin verme. Önemli tooallow ayrıntılı kesimleme budur. Örneğin, Pazarlamacılar hello tükettiği içerik türüne göre bir segmente yerleştirebilir. içerik türünü Hello hello dinamik bilgilerinin bir etkinlik veya bir olay olacaktır.

*Uygulama bilgileri* Merhaba uygulaması veya hello kullanıcı tooconfirm hello durumu gerçek zamanlı olarak verir verilerdir. Bu aynı zamanda hedef kitle tabanını toocategorize yardımcı olur ve hızlı bir şekilde. Örneğin, bunu hello kullanıcı veya oturum açmayı veya kendi abonelik sona erme tarihi doğru/yanlış durumunu kullanabilirsiniz.

#### <a name="example-of-tags"></a>Etiket örneği
*Kullanım örneği: Segment İzleyici davranışı tootarget hello doğru son kullanıcıyla hello doğru anında iletme bildirimi içeriği*

1. Bir ürün kategorisini anında iletme bildirimi toopromote gönder: hello ziyaret ettikleri ürün kategorisine göre dayalı davranışı veri toosegment İzleyici toplayın x kez belirli bir dönem veya bunlar ekledikleri içinde belirli bir öğe. toplanan hello verileri toosegment izin vermek ve ardından bir anında iletme bildirimi toohello doğru hedef kitleye'ni gönderin.
2. Oranı hello uygulama: sosyal ağ üzerinde hello İzleyici tarafından paylaşılan hello içerik göre verileri toplar. Amaçlar toosegment hello İzleyici hello belirleyerek *elçilerini* , uygulamanızın. Bir anında iletme bildirimi uygulama kullanıldığında hello elçiler, uygulama tooask toorate hello deposunda uygulamanızı 5 yıldız en iyi hedef kitle hello'dır.
   
   ![][1]

*Kullanım örneği: Bildirim temelli veriler*

1. Uyarı haberleri segmenti oluşturun: bildirim temelli veriler toosegment hedef kitleyi tercihlerine göre topla. Belirli bir kitleyi gerçekten ilgilendiren belirli bir konuda anında iletme bildirimi gönderilmesine olanak tanır.
2. Oturum açma durumuna göre hedef kitleyi segmentlere ayırın. Bir kullanıcının bağlı olduğu veya hesap oluşturup oluşturmadığını veri tooknow toplayın. Henüz oturum açmamış olan hedeflenmesine yardımcı olur ve bir anında iletme bildirimi tooencourage son kullanıcı tooconvert gönderir.
   ![][2]

### <a name="next-steps"></a>Sonraki adımlar
* Ziyaret [Mobile Engagement kavramları] toolearn temel Mobile Engagement kavramları hakkında daha fazla bilgi.
* Ziyaret [Mobile Engagement uygulaması oluşturma](mobile-engagement-create.md) toocreate Azure ve hello Mobile Engagement portalıyla uygulamalarınızı yönetmeye başlangıç yeni bir Mobile Engagement uygulama koleksiyonu.
* Ziyaret [en iyi uygulamalar](mobile-engagement-getting-started-best-practices.md) ayrıntıları içine toogo.
* Ziyaret [oyun uygulaması senaryosu](mobile-engagement-gaming-scenario.md) örnek bir oyun uygulaması ile Mobile Engagement'ı uygulama hakkında toolearn. 
* Ziyaret [medya uygulaması senaryosu](mobile-engagement-media-scenario.md) örnek bir medya uygulaması ile Mobile Engagement'ı uygulama hakkında toolearn. 
* Ziyaret [öğreticileri] toolearn hello uygulaması hakkında daha fazla.

<!-- Images. -->
[1]: ./media/mobile-engagement-define-your-mobile-engagement-strategy/use-case1.png
[2]: ./media/mobile-engagement-define-your-mobile-engagement-strategy/use-case2.png

<!-- URLs. -->
[Mobile Engagement kavramları]: http://azure.microsoft.com/documentation/articles/mobile-engagement-concepts/
[öğreticileri]: http://azure.microsoft.com/documentation/articles/mobile-engagement-ios-get-started/

