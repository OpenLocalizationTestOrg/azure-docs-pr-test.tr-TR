---
title: "aaaAzure Mobile Engagement Başlangıç Kılavuzu en iyi uygulamalar"
description: "Ekleme için En İyi Uygulamalarla Azure Mobile Engagement Başlangıç Kılavuzu"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure Mobile Engagement - En İyi Uygulamalarla Başlangıç Kılavuzu
## <a name="overview"></a>Genel Bakış
**Merhaba mobil ekran çok kalabalık bir yer:** hello ortalama bir mobil cihazda 27 uygulama yüklü olan bir olay incelemesi 2013'te bulundu. Kullanıcılar yükledikleri uygulamalarda genelde aylık 30 saat vakit harcıyor. Bu sürenin çoğunu sosyal ağlarda ve oyun oynama amacıyla harcanıyor (yaklaşık 20 saat). 2014 yılına gelindiğinde, hello Android markette kullanıcıların toochoose yaklaşık 1,5 milyon uygulama vardı. Merhaba Apple mağazası yaklaşık 1,2 milyon uygulama içeriyordu. Geliştiricilerin bu büyüyen pazarda rekabeti devam ederken mobil uygulama kullanımı hala artmaktadır. 

Merhaba ortalama bir mobil kullanıcı yüklemek ve sık değişen ilgi alanları bağlı olarak uygulamalarla kaldırmak ve uygulama içi deneyimlere. Itanium tabanlı sistemler için sipariş toodetermine hello başarılı bir uygulamanın şekilde bu önemli tooknow duruma daha çok ne kadar çok sayıda kullanıcı, uygulama yükleme. Önemli tooknow uygulamanızın ve kullanım eğiliminin değişip değişmediğini nasıl yararlı olur. Aşağıdaki sorular hello önemli hale gelmiştir:

* Kullanıcılarınızın toofind uygulamanızı sizi ilgilendirmeyen ya da artık kullanılmayan başlıyor? 
* Toplamda kaç kullanıcı uygulamanızı kullanmayı bıraktı? 
* Uygulama içi satın alma eğilimi artıyor mu yoksa azalıyor mu?
* Kullanıcıların toocomplete iş akışlarıyla hello uygulama veya ilgi eksikliği sorunları nedeniyle başarısız oluyor? 
* Uygulamanızı faydalı ve ilgili yeni içerik tooyour kullanıcı temel ileterek güvenliğinizi? 
* Bu yeni içerik tüm kullanıcılar için aynı veya uygulamanızdaki davranışa göre kullanıcı kesimlerine odaklanmıştır hello mu? 

Yanıtlar tooquestions benzer toothese uygulamanızdan hello ömrünü ve gelirini sürdürmeye yardımcı olabilir. Bunlar kullanıcı tabanınızı tanımlamanıza ve tutmanıza da yardımcı olur. 

Medya ilgili uygulamalar eğilimindedir toohave bazı kullanıcılar arasında en yüksek elde hello. Bunun bir nedeni, sürekli yeni içerik toousers sağlama ' dir. Kullanışlı anında iletme bildirimlerinin erken uyarlanması uygulama elde tutma üzerinde yüksek etkisi toohave tooa kullanıcı kesiminin eğilimlidir yönlendirilmiş. 

Merhaba ömrünü ve uygulamanızın elde tutulmasını yöntemi toogather sağlayarak genişletir ve hello kullanımı hakkında ayrıntılı bilgi, uygulamanızın analiz tasarlanmış toohelp Hello Azure Mobile Engagement programdır. Toobehavior göre kullanıcı tabanınızı sınıflandırmak ve tooidentified kullanıcı kesimlerine anında iletme bildirimleri ve uygulama içi iletiler teslim etmek için odaklı Kampanyalar oluşturmanıza yardımcı olur. Önemli Performans Göstergeleri (KPI) kullanıcılarınızın uygulamanızın farklı yönlerinde nasıl etkin olduğunu ölçer. Azure Mobile Engagement hello yöntemler sağlar bu KPI'leri toodetermine gerekir. Merhaba return artırmaya yardımcı olur, mobil uygulamanızı tooincrease katılım ihtiyacınız hello altyapısı sağlayarak, yatırımınızın (ROI) üzerinde. 

Sipariş tooget hello Azure Mobile Engagement en dışında iyi tasarlanmış bir katılım planıyla toostart gerekir. Planınız toobe mümkün toosegment kullanıcı temel ihtiyacınız olacak hello parçalı verileri belirlemenize yardımcı olur. Bu davranışı ya da uygulama için deneyimleri temel alabilir. Başarılı, planı toobe için bu en iyi yöntem tooclearly hello uygulamanızın hello hedeflerini ölçecek KPI tanımlamak sıradadır. Tanımlanan NET Performans göstergeleriyle kolayca hangi şunları yapacaksınız uygulama toocollect ince tanecikli verilerinizi hello gerekli mantığı eklenebilir, KPI'ları değerlendirmek ve tooanalyze kullanın. Bu konu, katılım planınızla kullanacağınız hello KPI'leri tanımlamaya ilişkin en iyi yöntem kılavuzluk edecektir. 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>Adım 1: KPI'ları toofit hello sonuç modelinizi tanımlayın
Kpı'lerin doğru şekilde tanımlanması zor bir görev toocomplete olabilir. Farklı sektörler için tasarlanan uygulamalar kendi özelliklerine ve hedeflerine sahiptir. Bu durum yaklaşımınızı tooconfuse eğilimlidir. toohelp bu kaçınmak için hedefler ve KPI'ler sınıflandırılmış üç ana kategoride: **iş**, **Engagement**, ve **teknik**. Merhaba veririz budur **BET modeli**.

İyi bir plan genellikle her kategori hello BET modelinin aşağıdaki hello hello başarıları ölçen hello KPI'ları hedeflere sahip olur.

#### <a name="business-kpis"></a>İş KPI'leri
İş KPI'leri hello kolay bölümü toobuild olmalıdır. Büyük olasılıkla mobil uygulamanızı planlarken bunu bir biçimde zaten tanımlamıştınız. Bu KPI’ler genellikle uygulamanız için geliri ve yatırım getirisiniz ölçmeye yardımcı olur. Merhaba aşağıdaki listede bazı örnek performans göstergelerinizi tanımlarken kılavuz yardımcı olabilecek iş KPI'leri verilmiştir:

* Medya İş KPI'leri
  * Tıklanan reklam sayısı
  * Kullanıcı başına sayfa ziyareti sayısı
  * Geçerli abonelik sayısı
* Oyun İş KPI'leri
  * Uygulama içi satın alma sayısı
  * Kullanıcı başına ortalama gelir (ARPU)
  * Oturum başına harcanan süre
  * Oynanan gün sayısı ve geçerli oyun düzeyi
* E-ticaret İş KPI'leri
  * Uygulamanın kullanıldığı gün sayısı
  * Kullanıcı başına ortalama gelir (ARPU)
  * Satın alma sırasında sepetteki ortalama tutar
  * En çok görüntülenme ve satın alma için ürün kategorisi
* Banka ve sigorta İş KPI'leri
  * Hesap sayısı
  * Etkinleştirilen özellikler
  * Ziyaret edilen teklif sayfaları
  * Tıklanan veya etkinleştirilen uyarı sayısı       

#### <a name="engagement-kpis"></a>Katılım KPI'leri
Katılım KPI'si kullanıcılarınızın performans göstergesi toomeasure hello katılım ' dir. Bu alandaki eğilimler uygulamanızın hello elde tutulmasını belirlemeye yardımcı olur. Burada bu tür KPI için bazı örnek performans göstergeleri verilmiştir:

* Merhaba son 7 gün içindeki etkin kullanıcılar
* Merhaba son 7 gün için etkin olmayan kullanıcı sayısı
* Merhaba uygulama 30 gün içinde kullanmamış kullanıcı sayısı  

Bazı bariz dış etkenler bu alandaki göstergeleri etkileyebilir. Örneğin, bir mobil cihaz toobe sahip bir kullanıcı her zaman düşünebilirsiniz. Bu doğru olabilir ya da olmayabilir. Bir oyun uygulaması toohave daha yüksek kullanım ne zaman bir oyuncu daha fazla hatayla iş veya Okul dışında oynayabilir tatiller geçici eğilimli olabilir.   

İyi tanımlanmış KPI'ler bu kategorideki yardımcı olması ölçmek hello uygulamanız ve müşterileriniz arasındaki ilişki.

#### <a name="technical-kpis"></a>Teknik KPI'ler
Bu kategorideki performans göstergeleri uygulamanızın doğru mu davrandığı, askıda mı yoksa çökmekte mi olduğunu belirlemenize yardımcı olur. Bu göstergeler uygulamanızın hello durumunu ölçebilir ve kullanıcıların hello uygulama kullanmalarına engel kullanılabilirlik sorunlarını belirleyebilir. Bu kategori için toplanan bilgiler, ilgili toomarketing takımlar olacaktır performans bilgilerini de içerebilir. Merhaba veri da tarafından sorun giderme için yararlı olabilir BT ve destek ekipleri toohelp bildirilmeyen hataları tanımlar. 

Bazı Teknik KPI örnekleri şunlardır:

* İşlenen veya işlenmeyen özel durum bilgileri ve sayısı 
* Son çökme için zaman damgası
* Tıklanan son düğme ya da ziyaret edilen son sayfa
* Merhaba uygulamanın bellek kullanımı
* Uygulama kare hızı
* Uygulama hello işletim sistemi sürümü çalıştıran
* Uygulama sürümü

Bu KPI'ları toohelp uygulama performansını tanımlayın ve potansiyel hataları bulmaya. Bu göstergeler toodeliver bir düzeltme müşterileriniz için gereksinim duyduğunuz hello süreyi azaltmaya Yardım etmelidir. Bunlar ayrıca belirli sorunlarla karşılaşan kullanıcı kesimini belirlemenize de yardımcı olabilir. Kullanılabilir düzeltmeler ve potansiyel promosyonlar toohelp ilgili kullanıcı kesimleme toocreate Kampanyalar toodeliver bildirimler müşteri memnuniyetini kurtarmak kullanabilirsiniz. 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>Playbook Alıştırması 1: KPI panonuzu oluşturma
Pazarlama stratejinizi tanımlarken, KPI'leriniz her bir ana hedefiniz için bir görünüm sunmalıdır. Bunlar, toocollect önemli bilgileri toomonitor hello son kullanıcı, uygulama ve hello davranışı olanak tanıyan NET tanımlanmış veri noktaları olmalıdır.

Merhaba aşağıdaki bilgileri içeren bir KPI panosu oluşturun

1. Hello KPI'leri hello uygulaması nedir?
2. Hangi veri noktalarını toorepresent her KPI kullanabilir miyim?
3. Bu veriler uygulamamda nerede yer alıyor (örn, ekran, ayarlar, sistem...)?
4. Bu KPI için Katılım sırası yürütebilir miyim?

Merhaba kullanabilirsiniz **KPI Builder** çalışma sayfasında bizim [Media Playbook şablonu] [ Media Playbook link] örnekler ve yönergeler.

## <a name="step-2-your-engagement-program"></a>2. Adım: Katılım Programınız
Mükemmel bir mobile engagement programı uygulamanız için temel bileşen kabul edilmelidir. Bu kesinlikle bir kullanıcı için ilk uygulama kullanımı gün sırasında hello yürüten harika bir karşılama programı içermelidir. Bu toohave katılımı ve bekletme, uygulamanızın üzerinde çok olumlu bir etkisi eğilimi gösterir. Çalışmalar, ilk birkaç gün sonra bir uygulama hello kullanarak kullanıcıların Dur hello çoğunluğu göstermiştir. Toostrive toomeet istediğiniz veya hello kullanıcı hala uygulamanıza odaklanırken müşteri beklentisi yönlendirmeli İlgiliyi erkenden aşıyor. Tooyour müşteriler hello anahtar değeri ve uygulamanızı avantajlarını sergilediğinizden emin olun. 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

Anında iletme bildirimleri hello en iyi yaklaşımı tooearly katılımlar mobil cihaz kullanıcılarıyla ' dir. Ancak, anında iletme bildirimleri için kullanıcılar kesimlenirken çok dikkatli olunmalıdır. Çünkü bir kullanıcının istenmeyen posta ya da ilgilenmediği bildirimler aldığını düşünmesinin ciddi etkileri olabilir. Birkaç tıklama ile bir kullanıcı uygulamanızı silebilir hiçbir zaman tooreturn. Merhaba kullanıcı genel istenmeyen posta yerine yüksek oranda kişiselleştirilmiş uygulama içi değer almalıdır.

Kullanıcılar etkin şekilde katıldığında, ardından katılım programınızı hello uygulama diğer yönlerini yönlendirmeye yardımcı olabilir.

Örneğin, etkin kullanıcılar toorate isteyen bir kampanya uygulamanızı Kurulum. Bu kullanıcı kesiminin hello en etkin ve en deneyimli uygulamanızı hello sahip olduğundan, bunları beklediğiniz toogive hello en doğru puanı. Yüksek uygulama puanı aldığınızda, de, yeni müşteri edinme maliyetlerini azaltmaya, uygulamanızın doğal indirilmesini hello sürücüyü yardımcı olabilir.

#### <a name="engagement-sequence"></a>Katılım Sırası
Genel bir Katılım programı farklı katılım sıraları içerir. Her sıra çeşitli hedeflere tooreach amaçlar.

###### <a name="life-push-sequence"></a>Ömür anında iletme sırası
Ömür anında İletme sırası Hello hedefleri hello kullanıcının katılım hello uygulamayla hello yaşam döngüsü bağlı olarak farklı olur. Belirli bir kullanıcı yeni, etkin olmayan veya çok etkin olabilir. Katılım yaşam döngüsünün farklı aşamalarında, kullanıcılar ipuçları veya bağlantılar toodocumentation hello biçiminde yeni içeriğinizde yararlı. 

Örneğin yeni bir kullanıcı ihtiyaç duyabileceğiniz Yardımı yönlendirilmiş tooan uygulama alma veya hello hello uygulamasını başlatın ilk kez izleyen bir yeni kullanıcı no'lu tebliğ kapsamında teşvik benzer toohello fayda...

*"Memnun toohave, yerleşik! Toologin tooget unutmayın, 1 aylık ücretsiz! "*

###### <a name="behavioral-push-sequence"></a>Davranışsal anında iletme sırası
Merhaba davranışsal İletme sırası hello uygulama için toplanan kullanıcı davranışı temel alan tooincrease kullanımı amaçlar.  

Örneğin, fantezi futbol uygulamasının etkin bir kullanıcı ile anında iletme bildirimi aşağıdaki hello gerçekleştiriliyor faydalanabilir...

*"John, tam bir futbol fanatiğisin! "Tooour NFL bölümünde oturum ve ücretsiz erişim toohello SuperBowl win!"*

###### <a name="alerting-push-sequence"></a>Uyarı anında iletme sırası
Kullanıcılar kendi ilgi alanlarına odaklanan ilgili haberlerden hoşlanacaktır. Uyarı anında iletme sırası, kullanıcının açık olarak gösterdiği ilgi alanları temelinde uyarıla göndererek katılımı artırır. Bir kullanıcı hello uygulamada kendi ilgili alanlarını seçtiğinde bu açık olabilir. Bu, örtük olarak hello uygulama ile kullanıcı etkileşimi sırasında toplanan verileri temel alan da belirlenemedi.

Örneğin, bir E-ticaret uygulaması hello kullanıcı belirli bir iş KPI'si ile yakaladığınız kahve markasını düzenli olarak satın alabilir. Merhaba aşağıdaki uyarı bu kullanıcının katılım hello uygulamayla geliştirebilirsiniz.

*"Merhaba Wes, sık kullanılan kahve markalarından biri birini olacaktır satış %25 hello kapalı Eylül 2015 ilk haftasında. Bir müşteri olarak veriyoruz ve toomake emin istedi, farkında."*

###### <a name="rentention-push-sequence"></a>Elde tutma anında iletme sırası
Bu sıra amaçlar tooretain kullanıcıları tekrarlayan anında iletme bildirimi kampanyaları toohelp kullanarak hello uygulamaya, normal bir alýþkanlýk sürücü. Bu, hello etkileşimleri hello kullanıcı hoşlanırsa, uygulama elde tutmayı artırmaya yardımcı olabilir. 

Örneğin, sporla ilgili bir uygulama hello kullanıcısı hello kullanıcının desteklediği takımlar temelinde haftalık temel anında iletme bildirimi aşağıdaki hello alabilirsiniz:

*"Hello New York Yankees'in kazanıp kazanamayacağına bu hafta Toronto Blue Jays'e karşı kazanır olup olmadığını fırsat toowin 200 puan, oy verin!"*

#### <a name="hello-3w-approach"></a>Merhaba 3W yaklaşımı
Merhaba farklı anında iletme sıralarını katılımınıza son kullanıcılarla yardımcı olur. Ancak, yine toouse hello 3W yaklaşımı bildirimlerinizi kişiselleştirmek için gerekir. Merhaba 3W yaklaşımı ilgilenmelidir kim, ne ve ne zaman her bir bildirim. Bu üç sorunu yanıtını tatmin edici şekilde karşıladığınızda, bildirimleriniz katılıma uygun şekilde odaklanmış olur.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>Kim: iletileri alacak kullanıcı kesimi hello
Bildirimleri tooyour kullanıcılar Ftp'den çok hassas bir iletişim kanalı olarak düşünülmelidir. Bu kullanıcı kesiminin ilgi iyi kapsamlı toohello toosend tooa kullanıcı kesiminin hedeflenir hello bildirimleri olduğundan emin olun. Yanlış yönlendirilmiş bir bildirimin kullanıcı üzerinde olumsuz etkisi büyük olasılıkla toohave ' dir. Kaldırılmakta tooyour uygulama önde gelen istenmeyen posta onu düşünebilirsiniz. 

İletileri alacak kullanıcı kesimlerini tanımlarken belirli teknik ve davranışsal ölçütlerin birleşimini kullanın. Bir kullanıcı kesimini tanımlamanın basit bir örnek deyiminden benzer toohello olabilir:

"Başlatılan tüm kullanıcılar bir mobil uygulama ilk kez 3 gün önce hello için hello ve iki kez gerçekte bir oturum açma tamamlamadan hello oturum açma sayfasını ziyaret etmiş".

Bu deyim toocollect toosupport belirli bir senaryoyu gerekir hello verileri tanımlamanıza yardımcı olur.

###### <a name="what-hello-message-that-you-will-send"></a>Ne: göndereceğiniz hello iletisi
**Ton**

Katılımlarınızda, kesimlenmiş kullanıcılarınız için uygun olarak bir ton kullanın. Bu kesinlikle kullanıcılarınıza ile en iyi yolu tooconnect ve uygulamanızı kullanıcının ilgi Yükselt. 

**Yönlendirme**

Anında iletme bildirimi birden fazla Merhaba uygulaması açmak için kullanılabilir. Toohello sağ doğrudan hello uygulamadaki içerik hello bildirim iletisi haber yayınlama gibi bir bağlam veya Ürün Tanıtımı, bu bildirim may ayrıntılı bağlantısı sağlar. toosupport Bu, bir URL oluşturmalısınız düzeni toolet hello uygulamasını Yönet hello yeniden yönlendirme. Katılım sıralarınızla çalışırken, bu unutulmaması gereken bir adımdır.

Yönlendirme diğer sistemler için de kullanılabilir. Örneğin, bir eylem URL'si ile olası tooredirect son kullanıcılar toomany olmasından hello aşağıdakiler dahil diğer sistemler:

* Web sitesi
* E-posta önceden ayarlı posta kutusu
* SMS kutusu
* Arama hizmeti
* Merhaba uygulama derecelendirme için doğrudan toohello uygulama deposu. 

Bu, birçok fırsatlar tooengage son kullanıcılar sağlar ve tooimprove performanslarını otomatik kurallar oluşturun.

**Biçim/İçerik**

Farklı türler ve Anında iletme bildirimi biçimleri:

1. **Duyurular** : farklı anlarda reklam iletileri toousers toosend sağlar (uygulama dışında uygulama veya herhangi bir zamanda).
2. **Anketler** : kendilerine sorular sorarak son kullanıcılar toogather bilgilerinden etkin. Bu yanıtlar daha sonra ölçütleri tootarget son kullanıcılar oluşturulurken kullanılabilir.
3. **Veri gönderimleri** : toosend bir ikili veya base64 veri dosyası tooupdate hello uygulaması sağlar. Veri gönderiminde yer alan hello bilgileri tooyour uygulama toopersonalize hello kullanıcı deneyimini uygulamanızda gönderilir. Veri gönderimi tasarlanmış toobe toosupport hello verileri uygulamanız gerekir.
4. **Kutucuklar (yalnızca Windows Phone)** : toouse hello Microsoft anında iletme bildirimi Hizmeti'ni (MPNS) toosend yerel anında iletilen bildirim (desteklenen SDK sürüm 0.9.0'dan itibaren. XML verileri içeren etkin kutucuklar için yük Hello 32 kilobaytı aşamaz.). Merhaba ileti doğrudan panonuzu'nın kutucuğu görüntülenir.
5. **Web görünümü** : Web görünümü web içeriği içeren açılır penceredir. Merhaba son kullanıcı hello anında iletme bildirimine tıkladığında bu açılır pencere görünür. Web görünümü toohave sağlar hello son kullanıcı ile daha fazla etkileşimi.

> [!NOTE]
> Anında iletme bildirimleri olarak gönderdiğiniz hello içerik uygulama geliştirme ve anında iletme bildirimleri gönderme yönergeleri hello ilgili platformun (göndermeye, Android, Windows) uygun olduğundan emin olun.
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>Ne zaman: kampanyanızın zamanlaması hello
Merhaba en iyi zaman tooactivate anında iletme bildirimini tetikleyen bir kampanyayı olduğunda? Bu el ile mi yoksa otomatik mi olmalı? Bu yinelenmeli mi? Belirleme hello doğru zamanı ve sıklığı hello en iyi sonuçlar temel tooengage kullanıcı sayısıdır. Her katılım sırası ve senaryosu için belirtmelisiniz hello en iyi zaman toosend anında iletme bildirimleri olacaktır. Bazı olası örnekler şunlardır:

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

Günlük olarak birçok bildirim gönderiyorsanız, kullanıcılarınızın gönderdiğiniz iletişimleri istenmeyen posta olarak algılayabileceğini dikkatle değerlendirmelisiniz. 

Azure Mobile Engagement gönderdiğiniz iletişimlerin istenmeyen posta olarak algılanmasını toohelp önlemek iki yöntem sağlar. İlk olarak, aynı kullanıcıların değil hedef hello yerine ince çizgisi kesimleme tooensure kullanın. Bunun yanı sıra, Azure Mobile Engagement bir "kota" özelliği de sağlar. Bu özellik bir kampanya için gönderilen bildirimleri sınırlayabilir. Örneğin, bir varsayılan kota too5 haftada ayarı hello kampanya kullanıcı kesiminin parçası bu hafta için en fazla 5 bildirimleri olarak eklene bir kullanıcının ilişkilendirilmesini sağlar.

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>Playbook Alıştırması 2: Kendi katılım programınızı oluşturma
Hedeflerinizi özetlemeye ve belirli sıraları kullanarak tooplay beklediğiniz hello kampanyaları tanımlamaya biraz zaman ayırın. Kampanyalarınızdaki hello 3W yaklaşımı toohello bildirimleri uyguladığınızdan emin olun. 

Kullanım hello **katılım programı** hello çalışma [Media Playbook şablonu] [ Media Playbook link] örnekler ve yönergeler.

## <a name="step-3-app-integration"></a>3. Adım: Uygulama Tümleştirmesi
#### <a name="create-a-tag-plan"></a>Bir etiket planı oluşturma
Azure Mobile Engagement toointegrate uygulamanıza toocreate bir etiket planı gerekir. Merhaba etiket planı hello dönüm hello projesinin ' dir. Pazarlama özellikleri, Merhaba uygulaması hello iş akışını ve hello uygulama toomeasure KPI'leri toplanan hello gerçek etiket verileri arasındaki hello ilişkiyi tanımlar. Hangi analizleri kullanarak şunları yapabilirsiniz gösterir toosee hello Portalı'nda. Ayrıca kullanıcı kesimlerini tanımlamanıza ve odaklı anında iletme bildirimleri tooengage son kullanıcılarınızı göndermek yardımcı olur. Tanımlanan hello etiket planı oluşturduktan sonra hello kod toointegrate ekleyerek uygulamanızı içine hello Azure Mobile Engagement SDK'sını kullanarak basit bir işlemdir.

Bir etiket planı uygulamadaki her şeyi etiketlememelidir. Yalnızca mobile engagement stratejinizin bir parçası olarak etiket verilerini içermelidir. Bu büyük olasılıkla uygulamalar arasında farklı olacaktır. Merhaba [Media Playbook şablonu] [ Media Playbook link] sağlanan Azure Mobile Engagement yardımcı tarafından belirtilen yöntemle bir etiket planı oluşturun. Kullanım hello **etiket planı** çalışma kılavuzu toobuilding olarak, etiket planı.

Merhaba çalışma sayfasında bir etiket bölümü tanımlarken, çok açık olun. Çok önemli tooavoid karışıklığı budur. Her bir etiketin gönderileceği her senaryoyu ayrıntılı olarak açıklayın. Her etiket burada katıştırılmış hello etkinlik Hello adını içerir. Bu tüm hello dahil edilmesi gereken **bilgi veren** hello çalışma parçası. Merhaba etiket planı çalışma sayfası test doğrulama için hello ana referans olmalıdır. 

Merhaba, **veri toocollect** bölümünde, Geliştirme ekibiniz hello türleri, adları, değerleri ve her biri için gerekli ek bilgiler anahtar/değer çiftlerini bulmalıdır katıştırılmış hello uygulamada.

Merhaba projeyle ilişkili tüm ekiplerle birlikte hello etiket planı incelemeniz önerilir. Gerekli düzeltmeleri yapın ve pazarlama ve geliştirme ekipleri için her şeyin net olduğunu onaylayın.

Merhaba **iş bildirimi** çalışma hello projeye dahil herkes kullanılan toohelp Kılavuzu olabilir.

#### <a name="data-types"></a>Veri Türleri
Bunlar Azure Mobile Engagement tarafından desteklenen ortak veri türleridir.

###### <a name="devices-and-users"></a>Cihazlar ve kullanıcılar
Azure Mobile Engagement, her cihaz için benzersiz bir tanımlayıcı oluşturarak kullanıcıları tanımlar. Bu tanımlayıcı, hello cihaz tanımlayıcısı (veya DeviceID) adı verilir. Aynı aygıt paylaşımın üzerinde çalışan tüm uygulamaların aynı cihaz tanımlayıcısını hello şekilde oluşturulur.

###### <a name="sessions-and-activities"></a>Oturumlar ve etkinlikler
Bir oturum hello uygulama bir kullanıcı tarafından çalıştırılan bir örneğidir. Merhaba oturum durduruluncaya kadar hello kullanıcı hello uygulamayı başlattığı hello zamandan yayar.

Bir etkinlik hello uygulama oturumu sırasında yapabilirsiniz noktalar kümesi mantıksal bir gruplandırmasıdır. Genellikle hello uygulama belirli bir ekranda olduğu, ancak hiçbir şey Merhaba uygulaması hello mantığı tarafından tanımlanan olabilir. En azından, uygulamanız için her ekranı veya Etkinliği etiketlemelisiniz. Bu, toounderstand hello kullanıcı yolu olanak tanır.

###### <a name="events"></a>Olaylar
Merhaba uygulama ile kullanılan tooreport kullanıcı etkileşimi olaylardır. Bunlar, içerik paylaşımı ya da bir video yürütme gibi anlık eylemler olabilir. Olayları etiketlemek, kullanıcıların hello uygulama ile nasıl etkileşim gösteren veri koleksiyonları sağlar. 

###### <a name="jobs"></a>İşler
İşler süresi olan kullanılan tooreport eylemlerdir. Bazı örnekler aşağıdakileri içerir:

* API çağrılarının yürütülmesi
* Reklamları görüntülenme zamanı
* Arka plan görevleri süresi 
* Satın alma işlemi süresi
* Video görüntüleme

###### <a name="errors"></a>Hatalar
Hataları hello uygulama tarafından algılanan kullanılan tooreport sorunlardır. Örneğin, yanlış kullanıcı eylemleri veya API çağrısı hataları.

###### <a name="application-information"></a>Uygulama bilgileri
Uygulama bilgileri (App-Info) kullanılan tooa kullanıcı deneyimini bir uygulamayla ilgili tootag verileri. Merhaba uygulama ile kullanıcı etkileşimi tarafından oluşturulur. 

Belirtilen uygulama bilgisi anahtarı için Azure Mobile Engagement yalnızca hello son değeri (Geçmiş yok) izler. Uygulama bilgisi uygulamanızın veya son kullanıcılarınızın hello durumunu gösterir. Örneğin hello oturum açma durumu veya kullanıcının sık kullanılan ürün grubu.

###### <a name="crash-data"></a>Çökme verileri
Kilitlenme verilerini otomatik olarak hello uygulama tarafından işlenmeyen uygulama hatalarını bildirir hello Mobile Engagement SDK'sı tarafından toplanır. Örneğin, meydana gelen işlenmeyen özel durum

###### <a name="extra-data"></a>Ek veriler
Parametrelerle geliştirilebilen olaylar, hatalar, etkinlikler ve işler. Ek bilgiler bir geliştirici Merhaba uygulaması alınan belirli veriler olarak sağlayabilir budur. Bu ayrıntılı kesimleme tanımlaması için önemlidir. 

Örneğin, bir "makale" etiketi hello değerini toosegment son kimin makaleyi görüntüleyenler temelinde izin verir. Ancak bu yeterli olmayabilir. Bu aynı “makale” etiketine, etkinlikte “news_category” gibi ekstra bilgi eklenirse daha iyi olabilir. Bu yararlı olur toodetermine hello kullanıcı için sık kullanılan kategorileri dinamik olarak hello. 

Ek bilgiler bir anahtar/değer çifti olarak bildirilir. Bu medya uygulaması Hello örnekte hello "news_category" ek bilgileri bu kategori için hello değer olacaktır. Örneğin, "spor", "ekonomi" veya "siyaset".

#### <a name="tag-and-sdk-integration"></a>Etiket ve SDK tümleştirmesi
Uygulamanıza Azure Mobile Engagement SDK'sını tümleştirmek için adım adım yönergeler hello için hello izleyin [Engagement SDK tümleştirmesi](mobile-engagement-windows-store-integrate-engagement.md) Azure Web sitesinde belgeleri. Merhaba sayfanın üst kısmındaki bu hello bağlantılardan hedef platformunuzu seçin.

Azure Mobile Engagement’ın en üstünde oluşturulan iki uygulama için proje oluşturmanızı öneririz. Biri geliştirme ve test hazırlama ve üretim hazırlama için diğer hello. BT ekibinizin hello kullanıcı kabul testi başarılı olduğunda tooproduction hazırlama testten sonra yükseltebilirsiniz.

#### <a name="user-acceptance-testing-uat"></a>Kullanıcı kabul testi (UAT)
Kullanıcı kabul testi (UAT) her şeyin tasarlandığı gibi çalıştığından emin olmayı içerir. İş akışları tamamlanabilir ve etiket planınız temelinde gerekli tüm veriler toplanır:

* Bilgi etiketleme toodocumented AZME kavramlarına göre yerinde olmalıdır
* Gereksinim duyduğunuz tüm bilgiler toplanır (Ek bilgi değeri, Uygulama bilgisi değeri dahil)
* Adlandırma according tooyout etiket planı eşleşir
* Gönderilen yinelenen etiket yok

Uygulamanızda katıştırılmış bildirim davranışı tüm hello türleri sınamanız

* Uygulama dışı ve uygulama içi Duyurular, Anketler, veri gönderimleri
* Metin/Web görünümleri
* Gösterge güncelleştirme, Kategoriler

#### <a name="setup"></a>Kurulum
Azure Mobile Engagement kurulumu çok kolaydır. Toohello kullanıcı arabirimidir hello Azure Mobile Engagement Web sitesinde bulunan tüm hello belgeleri ilgili [nasıl toonavigate hello kullanıcı arabirimi](mobile-engagement-user-interface-home.md).

Merhaba doğru rolleri ve projenizin hello kullanıcıları için rol üyeliklerini ayarlayarak başlamanız önerilir. Tüm kullanıcılar için uygun erişim toohello platform yönetmenize yardımcı olur. Rolleriniz şunları içerebilir:

* Yöneticiler
* Geliştiriciler
* Görüntüleyiciler 

Daha sonra:

* Kendi Cihazınızda, DeviceID tootest kaydedin.
* Hesap toohello ayarlarınıza gidin ve hello saat dilimi toohave grafikler ve bildirim teslim saati, saat dilimini ayarlayın.
* Uygulama toohello ayarlarınıza gidin ve "App-info Reach dahilindeki tootarget son kullanıcı gerekir" Merhaba kaydedin.

Toorun ilk nasıl anında iletme hakkında daha fazla bilgi için bildirim kampanyası, gözden geçirme [nasıl tooget kullanılarak başlatılan ve yönetme iter tooyour son kullanıcılar çıkışı tooreach](mobile-engagement-how-tos.md).

## <a name="conclusion"></a>Sonuç
Katılım Programları yinelemelidir ve uygulamanız için en çok işe yarayan deneyiminizle kendinizinkini sürekli geliştirmelisiniz. 

Deneyimi Geliştirme sırasında başlangıçta, katılım ile toobuild tüm genel katılım stratejisi stratejileri denemeyin. Kpı'lerinizi tanımlayan adım adım bir yaklaşım uygular ve nasıl tooleverage bunları. Katılım stratejisi her uygulama için benzersiz olacaktır.

Biraz deneyim kazandıktan sonra aşağıdaki tooyour katılım programları hello eklemeyi düşünebilirsiniz:

* İzleme: Kullanıcılar alır ve büyük olasılıkla veri koleksiyonu kaynakları tanımlarsınız. Azure mobile Engagement, bağlı toodata koleksiyon kaynakları olabilir. Her kaynağında performansını toomonitor sağlar. Bu bilgiler edinme yatırımınızı ilginç toomaximize olacaktır. 
* A / B testi: Bu, Katılım programının temel bir parçasıdır. Her uygulamanın kendi özellikleri vardır. A/B testi ile, katılım programınızı geliştirebilirsiniz.
* Coğrafi konum: Bu, markalar için büyük bir fırsattır. Teşekkür ederiz toothis özelliği hello doğru yerde ve zamanda ulaşabilirsiniz. Toouse coğrafi konum başlamadan önce yeterli son kullanıcı davranışı verisi topladığınızı doğrulamanızı öneririz.
* Veri gönderimi: Veri gönderimi görünmez bir anında iletimdir. Veri gönderimi sonu kullanıcı davranışı temelinde uygulamanızı özelleştirmenize olanak tanır. Örneğin, bir kullanıcı kesimi genellikle yüksek teknoloji ürünlere başvuruyorsa, hello uygulama sahibi kendi giriş sayfasını yüksek teknoloji içeriğiyle kişiselleştirecek bir veri gönderimi gönderebilir.

## <a name="next-steps"></a>Sonraki Adımlar
* [Azure Mobile Engagement hesabı oluşturma](mobile-engagement-create.md).
* Ziyaret [Mobile Engagement stratejinizi tanımlama](mobile-engagement-define-your-mobile-engagement-strategy.md) toolearn Mobile Engagement stratejinizi tanımlama hakkında daha fazla bilgi.

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
