---
title: "aaaIoT güvenlik mimarisi | Microsoft Docs"
description: "IOT güvenlik mimarisi yönergeleri ve ilgili önemli noktalar"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 18ed3eb0-9406-44e1-8a3a-93dc6726c7ac
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: 5b59133f6b1b45573318c3bd5b621d27b147d71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-architecture"></a>Nesnelerin interneti güvenlik mimarisi
Sistem tasarlanırken önemli toounderstand hello olası tehditler toothat sistemidir ve hello sistem tasarlanmış ve tasarlanmış gibi uygun savunma buna göre ekleyin. Toodesign hello hello başlangıç üründen göz önünde bulundurularak ile nasıl bir saldırganın mümkün toocompromise bir sistem olabilir anlama uygun Azaltıcı Etkenler hello başından yerinde olduğundan emin olun yardımcı olduğu için özellikle önemlidir. 

## <a name="security-starts-with-a-threat-model"></a>Bir tehdit modeli ile güvenlik başlar
Microsoft tehdit modelleri ürünlerinden için uzun kullandı ve herkese açık işlem modelleme hello şirketin tehdit sunmuştur. Merhaba şirket deneyimi hello modelleme olduğunu gösteren hello hangi tehditleri hello olan çoğu ilgili anlama hemen ötesinde beklenmeyen avantajları. Örneğin, ayrıca bir açık tartışma için bir avenue başkalarıyla toonew fikirleri ve geliştirmeleri hello üründe açabilir hello geliştirme ekibi dışında oluşturur.

Merhaba amacı tehdit modelleme, bir saldırganın nasıl ve mümkün toocompromise bir sistem olabilir uygun Azaltıcı Etkenler karşılandığından emin olun toounderstand ' dir. Tehdit modelleme hello sistem tasarlandığı gibi hello Tasarım ekibi tooconsider Azaltıcı zorlar yerine bir sistemi dağıtıldıktan sonra. Güvenlik savunmaları tooa çözümlenebilen cihazların Merhaba alanında retrofitting uyuşmazlığa, olgunun kritik düzeyde önemli olduğundan hataya ve müşteriler risk bırakır.

Birçok geliştirme ekiplerinin müşteriler yararlanan hello işlevsel hello sistemi gereksinimleri yakalama mükemmel iş yapın. Ancak, birisi hello sistem kötüye belirgin olmayan yolları tanımlayan daha zordur. Tehdit modelleme geliştirme ekiplerinin bir saldırgan ne anlamanıza yardımcı olabilir ve neden. Tehdit modelleme hello güvenlik hakkında tartışma tasarım kararları hello sistem yanı sıra güvenlik etkisi hello yol boyunca yapılan değişiklikleri toohello tasarım oluşturan yapılandırılmış bir işlemdir. Bir tehdit modeli yalnızca bir belge olsa da, bu belgeleri de bilgi, dersleri bekletme tooensure devamlılığı öğrenilen ve yerleşik yeni takım hızlı bir şekilde Yardım ideal bir yolunu temsil eder. Son olarak, bir tehdit modelleme sonucunu tooenable olduğundan, tooconsider hangi güvenlik taahhütleri tooyour müşteriler tooprovide istediğiniz gibi güvenlik, diğer yönlerini. Tehdit modelleme ile birlikte bu taahhüt bildirin ve nesnelerin interneti (IOT) çözümünüzün sınama sürücü.

### <a name="when-toothreat-model"></a>Zaman toothreat modeli
[Tehdit modelleme](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) hello tasarım aşaması dahil edilmiş, teklifleri hello en büyük değer. Tasarlarken, hello en büyük esnekliği toomake değişiklikleri tooeliminate tehditlere sahip. Tehditler tasarım gereği ortadan hello istenen sonuca olur. Azaltıcı Etkenler ekleme, bunları test etme ve geçerli kalır ve ayrıca, bu tür eleme her zaman mümkün değildir sağlayarak daha çok daha kolay olur. Bu tehditler bir ürünün daha fazla olduğunda yetişkin ve sırayla sonuçta daha fazla iş ve önceden hello geliştirme modelleme tehdit daha çok daha zor dengelemeden gerektirir daha zor tooeliminate olur.

### <a name="what-toothreat-model"></a>Hangi toothreat modeli
Model hello çözüm tam ve ayrıca alanları aşağıdaki hello odakta olarak iş parçacığı:

* Merhaba güvenlik ve gizlilik özellikleri
* Merhaba özellikleri, hataları ilgili güvenlik
* güven sınırının touch hello özellikleri 

### <a name="who-threat-models"></a>Kimin modelleri tehdit
Tehdit modelleme gibi başka bir işlemdir.  Bir fikir tootreat hello tehdit modeli belge hello çözümün herhangi bir bileşeni gibi ve doğrulamak. Birçok geliştirme ekiplerinin müşteriler yararlanan hello işlevsel hello sistemi gereksinimleri yakalama mükemmel iş yapın. Ancak, birisi hello sistem kötüye belirgin olmayan yolları tanımlayan daha zordur. Tehdit modelleme geliştirme ekiplerinin bir saldırgan ne anlamanıza yardımcı olabilir ve neden.

### <a name="how-toothreat-model"></a>Nasıl toothreat modeli
İşlem modelleme hello tehdit dört adımdan oluşur; Merhaba adımlar şunlardır:

* Model Merhaba uygulaması
* Tehditler listeleme
* Tehditlerin azaltılmasına
* Merhaba Azaltıcı doğrula

#### <a name="hello-process-steps"></a>Merhaba işlem adımları
Üç kuralları altın tookeep bir tehdit modeli oluşturulurken unutmayın:

1. Referans Mimarisi dışında bir diyagram oluşturun. 
2. Avantajlarına ilk başlatın. Genel bir bakış elde ve derin girmeden önce bir bütün olarak hello sistem anlayın.  Bu yardımcı olur, derin Dalış hello sağ yerleştirir emin olun.
3. Merhaba işlem sürücü, hello işlemi, sürücü izin vermeyin. Bir sorun aşaması modelleme hello bulmak ve tooexplore istiyorsanız, bunun için gidin!  Toofollow adımları slavishly gereksinim düşündüğünüz yok.  

#### <a name="threats"></a>Tehditleri
bir tehdit modeli Hello dört temel öğeleri şunlardır:

* İşlemler (web Hizmetleri, Win32 hizmetleri * nix Daemon, vs. Bir işlem teknik ayrıntıya olduğunda bu alanlarda mümkün değil gibi bazı karmaşık varlıklar (örneğin alan ağ geçitleri ve algılayıcılar) soyutlanması unutmayın.
* Verileri (her yerden bir yapılandırma dosyası veya veritabanı gibi veriler depolanır) depolar
* Veri akışı (burada veri hello uygulamada diğer öğeler arasında taşır)
* Dış varlıklar (Merhaba sistemiyle etkileşimli herhangi bir şey ancak Merhaba uygulaması hello denetimi altında örnekler kullanıcıları eklemek ve uydu akışları)

Merhaba mimari diyagramı tüm öğelerin konu toovarious tehditleri; yine de uygun istiyor musunuz? Merhaba STRIDE anımsatıcı kullanacağız. Okuma [yeniden tehdit modelleme, STRIDE](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) tooknow hello STRIDE öğeler hakkında daha fazla.

Konu toocertain STRIDE tehditleri hello uygulama diyagramı farklı öğeler şunlardır:

* Konu tooSTRIDE işlemlerdir
* Veri akışları konu tooTID olan
* Merhaba veri depolarına günlük dosyalarını veri depolarına konu tooTID ve bazen R, bağlanırlar.
* Konu tooSRD dış varlıklardır

## <a name="security-in-iot"></a>IOT güvenlik
Bağlı özel amaçlı cihazlar çok sayıda olası etkileşim yüzey alanlarını ve her biri tooprovide toothose aygıtları sayısal erişim güvenliğini sağlamak için bir çerçeve düşünülmelidir etkileşim düzenleri sahip. Merhaba "dijital erişim" doğrudan aygıt etkileşiminin gerçekleştirilen herhangi bir işlem gelen kullanılan burada toodistinguish erişim güvenliği fiziksel erişim denetimi aracılığıyla burada sağlanan bir terimdir. Örneğin, hello cihaz kilit bir odada içine hello kapının koyma. Fiziksel erişim, yazılım ve donanım kullanarak kısıtlanamaz olsa da, ölçüleri toosystem girişim önde gelen tooprevent fiziksel Access'ten alınabilir. 

Biz hello etkileşim desenleri keşfetmenizde "cihaz denetimine" ele alacağız ve dikkat aynı düzeyde olan "cihaz verileri" Merhaba. "Aygıt denetimi" tooa aygıt değiştirilmesi ya da kendi veya kendi ortamının hello durumda doğrultusunda davranışını etkileyen hello hedefi herhangi bir şirket tarafından sağlanan herhangi bir bilgi olarak sınıflandırılabilir. "Cihaz verileri" bir aygıt, durumu ve onun ortamı durumunu gözlenen hello hakkında diğer taraf tooany yayar herhangi bir bilgi olarak sınıflandırılabilir.

Sipariş toooptimize en iyi güvenlik uygulamaları, tipik bir IOT mimarisinin alıştırma modelleme hello tehdit bir parçası olarak birkaç bileşen/bölgelere ayrılmasına önerilir. Bu bölgeler tam olarak bu bölümde açıklanan ve şunları içerir:

* Cihazı
* Alan ağ geçidi
* Bulut, ağ geçitleri ve
* Hizmetler.

Bölgeleri geniş şekilde toosegment bir çözüm; her bölge genellikle kendi veri ve kimlik doğrulama ve yetkilendirme gereksinimlerine sahiptir. Bölgeler ayrıca kullanılan tooisolation gibi zarar ve yüksek güven bölgeleri düşük güven bölgelerinde hello etkisini kısıtlayın.

Her bölge bir güven hello hello diyagrama kırmızı satırda noktalı olarak hangi belirtilir sınır ile ayrılır. Bir kaynak tooanother veri/bilgileri geçişin temsil eder. Bu geçiş sırasında hello veri/bilgileri konu tooSpoofing, kurcalama, ret, bilgi açıklama, hizmet reddi ve ayrıcalık yükseltme (STRIDE) olabilir.

![IOT güvenlik bölgeleri](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Merhaba her bir sınır içinde gösterilen de tabi tooSTRIDE tam 360 etkinleştirme bileşenleridir hello çözüm görünümünü modelleme tehdit. Aşağıdaki bölümler Hello ayrıntılı şekilde her biri hello bileşenleri ve belirli güvenlik sorunları ve yerine sokulmalıdır çözümler.

izleyin hello bölümler genellikle bölgelerinde bulunan standart bileşenleri ele alınacaktır.

### <a name="hello-device-zone"></a>Merhaba aygıt bölge
Merhaba aygıt hello hemen fiziksel alan ortamıdır, fiziksel erişim ve/veya "yerel ağ" eşler arası dijital eriştiği toohello hello aygıt uygun aygıttır. "Yerel ağ" toobe farklı ve gelen – yalıtılmış ancak büyük olasılıkla çok – hello genel Internet bağlantı ve aygıtların eşler arası iletişime izin verir herhangi mesafeli Kablosuz radyo teknolojisi içeren bir ağ varsayılır. Mevcut *değil* yerel bir ağ hello atmosferini oluşturma tüm ağ sanallaştırma teknolojisini içerir ve ortak ağ alanında herhangi iki aygıtları toocommunicate gerektiren genel işleç ağları da içermez Bunlar tooenter bir için eşler arası iletişim ilişkisi varsa.

### <a name="hello-field-gateway-zone"></a>Merhaba alan ağ geçidi bölge
Alan ağ geçidi aygıtı/gereç ya da iletişim etkinleştiricisi olarak ve da potansiyel olarak, aygıt denetim sistemi ve aygıt veri işleme hub gibi davranan bazı genel amaçlı sunucu bilgisayar yazılımı olur. Merhaba alan ağ geçidi bölge hello alan ağ geçidi kendisini içerir ve tüm cihazlar tooit bağlı. Hello adından da anlaşılacağı gibi alan ağ geçitleri dış özel veri işleme tesis hareket, genellikle konumu bağlı, büyük olasılıkla konu toophysical yetkisiz erişim olduğunu ve işletimsel artıklık sınırlı olur. Bir alan ağ geçidi genellikle olan tüm toosay bir şey dokunma ve onun işlevini nedir bilerek sabotage. 

Bir alan ağ geçidi erişimi yönetme etkin bir rol oluşturdu ve bilgi akışını uygulama olduğu anlamına gelir, varlık ve ağ bağlantınızı veya terminal oturumu ele yalnızca trafik yönlendiriciden farklıdır. Bunlar açık bir bağlantı veya oturum Terminal, ancak bunun yerine bir yol (veya blok) bağlantıları olmayan bu yana bir NAT cihazı veya güvenlik duvarı, buna karşılık, alan ağ geçidi olarak nitelemek değil ya da bunları yapılan oturumları. Merhaba alan ağ geçidi iki ayrı yüzey alanı yok. Bir bağlı tooit hello cihazlar bakarken hello bölge içinde hello temsil eder ve hello diğer tüm dış tarafların bakarken ve hello ucunun hello bölgenin.   

### <a name="hello-cloud-gateway-zone"></a>Merhaba bulut ağ geçidi bölge
Bulut ağ geçidi genellikle bir bulut tabanlı denetim ve veri analizi sistem, bu sistemlere Federasyonu doğrultusunda ortak ağ alanı üzerinden uzaktan iletişimi ve birkaç farklı sitelerin toodevices veya alan ağ geçitleri sağlayan bir sistemdir. Bazı durumlarda, bir bulut ağ geçidi hemen erişim toospecial amacı Terminal tabletler veya telefonlar gibi aygıtlardan kolaylaştırabilir. Ele alınan hello bağlamda burada "bulut" Merhaba aygıtları veya alan ağ geçitleri bağlı olarak aynı site ilişkili toohello değil toorefer ayrılmış tooa veri işleme sistem amaçlanmıştır. Ayrıca bulut bölgesinde işletimsel ölçüleri hedeflenen fiziksel erişimi engellemek ve mutlaka gösterilen tooa "Genel bulut" altyapı olup olmadığı.  

Bulut ağ geçidi, ağ sanallaştırma katmana tooinsulate hello bulut ağ geçidi ve tüm bağlı aygıtları veya alan ağ geçitleri üzerinden diğer ağ trafiğinden potansiyel olarak eşlenebilir. Merhaba bulut ağ geçidinin kendisi ne aygıt denetim sistem ya da bir işleme veya depolama tesisi cihaz verileri için olan; Bu olanakları ile Merhaba bulut Ağ Geçidi Arabirimi. Aygıt tooit doğrudan veya dolaylı olarak bağlı ve hello bulut ağ geçidinin tüm alan ağ geçitleri ile birlikte Hello bulut ağ geçidi bölge içerir. Merhaba bölge Hello kenarı, tüm dış tarafların üzerinden iletişim kurduğu ayrı bir yüzey alanıdır.

### <a name="hello-services-zone"></a>Merhaba Hizmetleri bölge
"Hizmet" Bu bağlamda herhangi bir yazılım bileşeni veya cihazlara sahip bir alan veya Bulut ağ geçidi üzerinden veri toplama ve analiz için yanı sıra komut ve denetim için arabirim modülü olarak tanımlanmıştır.  Ortam araçları hizmetleridir. Bunlar kimliklerini ağ geçitleri ve diğer alt sistemleri doğrultusunda altında hareket, depolamak ve verileri çözümlemek, sınırlarına sorunu komutları toodevices veri Öngörüler veya zamanlamaları göre ve bilgi ve denetim özellikleri tooauthorized son kullanıcıların kullanımına sunma.

### <a name="information-devices-vs-special-purpose-devices"></a>Özel amaçlı cihazlar ve aygıtlarını bilgiler
Bilgisayarlar, telefonlar ve tabletler öncelikle etkileşimli bilgi aygıtlardır. Telefonlar ve tabletler açıkça pil ömrü en üst düzeye çıkarma geçici hale getirilmiştir. Bunlar tercihen kısmen hemen bir kişiyle kullanılırken ya da tooa belirli konum müzik çalma veya kendi sahibi yönlendirmede gibi hizmetleri sağlayan değil kapatın. Sistemleri açısından bakıldığında, bu bilgi teknolojisi cihazlar proxy'leri kişiler doğru olarak esas olarak çalışıyor. "Kişiler erişim düzenekleri eylemleri ve"kişiler algılayıcılar giriş toplama"öneren" oldukları. 

Özel amaçlı cihazlar basit sıcaklık algılayıcıları toocomplex Fabrika üretim satırlarından bileşenleri içerdikleri, binlerce farklıdır. Bu cihazlar çok daha amacı kapsamlı ve bazı kullanıcı arabirimi sağladıkları olsa bile, büyük ölçüde kapsamlı toointerfacing sahip olan veya fiziksel Merhaba Dünya varlıkları tümleştirilmesini. Bunlar ölçmek ve ortam koşullar raporu, vanalar açın, servos denetlemek, alarmlar ses, ışık geçin ve birçok diğer görevleri yapmak. Bunlar, iş toodo bilgi cihaz çok genel, çok pahalı, çok büyük veya çok kırılır yardımcı olur. Merhaba somut amacı, teknik tasarımlarını hemen zamanlanmış ömrü işlemi ve üretim için kullanılabilir parasal bütçe iyi hello olarak belirler. Bu iki önemli faktör Hello birleşimi hello kullanılabilir işletimsel enerji bütçe, fiziksel ayak izini ve böylece kullanılabilir depolama, hesaplama ve güvenlik özellikleri kısıtlar.  

Bir şeyler olursa "gelecek yanlış" aygıtlarla otomatik olarak veya uzaktan denetlenebilir, örneğin, fiziksel hataları veya Denetim mantığı kusurları toowillful yetkisiz erişim ve düzenleme yetkisiz. Merhaba üretim çok yok edilmesi, binalar looted veya Yakılan ve kişiler yaralı ve hatta özel olabilir. Bu, doğal olarak, bir tam farklı birisi bir çalınan Kredi kartının sınırı maxing daha kesimin sınıftır. Merhaba şeyler yapın aygıtlar için güvenlik çubuğunu taşıyın ve ayrıca algılayıcı verilerini sonunda şeyler toomove neden komutları sonuçlarında, herhangi bir e-ticaret veya banka senaryosu daha yüksek olması gerekir. 

### <a name="device-control-and-device-data-interactions"></a>Aygıt denetimi ve aygıt veri etkileşimleri
Bağlı özel amaçlı cihazlar çok sayıda olası etkileşim yüzey alanlarını ve her biri tooprovide toothose aygıtları sayısal erişim güvenliğini sağlamak için bir çerçeve düşünülmelidir etkileşim düzenleri sahip. Merhaba "dijital erişim" doğrudan aygıt etkileşiminin gerçekleştirilen herhangi bir işlem gelen kullanılan burada toodistinguish erişim güvenliği fiziksel erişim denetimi aracılığıyla burada sağlanan bir terimdir. Örneğin, hello cihaz kilit bir odada içine hello kapının koyma. Fiziksel erişim, yazılım ve donanım kullanarak kısıtlanamaz olsa da, ölçüleri toosystem girişim önde gelen tooprevent fiziksel Access'ten alınabilir. 

Biz hello etkileşim desenleri keşfetmenizde "cihaz denetimine" ele alacağız ve tehdit modellemesi çalışırken dikkat aynı düzeyde olan "cihaz verileri" Merhaba. "Aygıt denetimi" tooa aygıt değiştirilmesi ya da kendi veya kendi ortamının hello durumda doğrultusunda davranışını etkileyen hello hedefi herhangi bir şirket tarafından sağlanan herhangi bir bilgi olarak sınıflandırılabilir. "Cihaz verileri" bir aygıt, durumu ve onun ortamı durumunu gözlenen hello hakkında diğer taraf tooany yayar herhangi bir bilgi olarak sınıflandırılabilir. 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>Tehdit modelleme Hello Azure IOT başvuru mimarisi
Microsoft Azure IOT modelleme toodo tehdit yukarıda özetlenen hello çerçevesi kullanır. Merhaba aşağıdaki bölümde bu nedenle Azure IOT başvuru mimarisi toodemonstrate nasıl tehdit modelleme IOT ve nasıl tooaddress tehditleri hello için hakkında toothink tanımlanmış somut örneği hello kullanırız. Örneğimizde dört ana odak alanı belirledik:

* Cihazlar ve veri kaynakları
* Veri taşıma
* Cihaz ve olay işleme ve
* Sunu

![Tehdit için Azure IOT modelleme](media/iot-security-architecture/iot-security-architecture-fig2.png) 

Merhaba diyagrama hello Microsoft tehdit modelleme aracı tarafından kullanılan bir veri akış diyagramı modeli kullanılarak Microsoft'un IOT mimarisinin basitleştirilmiş bir görünümünü sağlar:

![Tehdit MS tehdit modelleme aracını kullanarak Azure IOT için modelleme](media/iot-security-architecture/iot-security-architecture-fig3.png)

Merhaba cihaz ve ağ geçidi özellikleri mimarisi hello toonote ayıran önemlidir. Bu daha güvenli olan ağ geçidi cihazların Merhaba kullanıcı tooleverage sağlar: gerektiren genellikle bir thermostat gibi-bir yerel aygıtı - verebilir, büyük işlem ek yüküne Güvenli protokoller kullanarak hello bulut ağ geçidi ile iletişim kurabilen kendi kendine sağlar. Hello Azure Hizmetleri bölgesinde bulut ağ geçidi hello Azure IOT Hub hizmeti tarafından temsil edilen o hello varsayıyoruz.

### <a name="device-and-data-sourcesdata-transport"></a>Aygıt ve veri kaynakları/veri aktarımı
Bu bölümde, tehdit modelleme hello Mercek yukarıda özetlenen hello mimarisi inceler ve nasıl biz bazı hello devralınmış sorunları ele alır genel bir bakış sağlar. Biz hello çekirdek öğeleri bir tehdit modeli üzerinde odaklanır:

* İşlemler (bizim denetim ve dış öğeler altında olanlar)
* (Veri akışları olarak da bilinir) iletişimi
* Depolama (veri depoları olarak da bilinir)

#### <a name="processes"></a>İşlemler
Her hello Azure IOT mimarisi ana hatlarıyla hello kategorileri, biz farklı tehditleri hello farklı aşamalar veri/bilgileri arasında bir sayı mevcut toomitigate deneyin: işlem, iletişim ve depolama. Aşağıda hello genel bir bakış nasıl bu en iyi şekilde azaltılması gereken genel bir bakış tarafından izlenen hello "işlem" kategorisi için en yaygın olanları sunuyoruz: 

**(S) yanıltma**: bir saldırganın bir aygıttan düzeyinde hello yazılım veya donanım ya da şifreleme anahtar malzemesi ayıklamak ve sonradan hello aygıt hello hello kimliğini altında farklı bir fiziksel veya sanal cihaz ile Merhaba sistemine erişim anahtar malzemesi gelen alınmış. Uzaktan herhangi TV kapatabilirsiniz ve popüler prankster araçları olan denetimleri buna iyi bir çizimidir.

**Engelleme, hizmet (D)**: bir aygıt çalışmıyor veya radyo frekansları veya kesme kablolarını uğratarak iletişim kuramadığı oluşturulabilir. Örneğin, özellikle gizleyen güç veya ağ bağlantısı olan bir izleme kamera verileri hiç bildirmez.

**(T) oynama**: bir saldırgan hello cihazda çalışan hello yazılım kısmen veya tamamen değiştirebilir, anahtar malzeme veya şifreleme hello hello yerine yazılım tooleverage hello orijinal kimliğini hello aygıt Merhaba, potansiyel olarak izin verme anahtar malzeme bulunduran tesis kullanılabilir toohello yasadışı program yoktu. Örneğin, bir saldırganın ayıklanan anahtar malzeme toointercept yararlanan hello iletişim yolunun hello aygıtta verilerden gizlemek ve çalınırsa hello anahtar malzemesi ile kimlik doğrulaması yanlış veri değiştirin.

**Bilgilerin açığa çıkmasına (ı)**: hello cihaz yönetilebilen yazılım çalışıyorsa yönetilebilen yazılımla olası veri toounauthorized tarafların sızıntısı. Örneğin, bir saldırganın ayıklanan anahtar malzeme tooinject kendisini hello iletişim yolunun hello aygıt denetleyicisi veya alan ağ geçidi arasında içine yararlanan veya ağ geçidi toosiphon bilgi kapalı bulut.

**Yükseltme, ayrıcalık (E)**: belirli bir işlevi gerçekleştiren cihaz zorlanmış toodo başka bir şey olabilir. Örneğin, tüm hello tooopen yarısı şekilde olabilir programlanmış tooopen olan bir Vana sağladı yolu.

| **Bileşen** | **Tehdit** | **Azaltma** | **Riski** | **Uygulama** |
| --- | --- | --- | --- | --- |
| Cihaz |S |Merhaba cihaz kimlik doğrulaması ve kimlik toohello aygıt atama |Aygıt ya da hello aygıt parçası başka bir aygıt ile değiştirin. Biz toohello doğru cihazlara Konuşmayı nasıl biliyoruz? |Aktarım Katmanı Güvenliği (TLS) veya IPSec kullanarak kimlik doğrulama hello aygıt. Altyapı önceden paylaşılan anahtar (PSK) kullanarak tam asimetrik şifreleme işleyemiyor bu cihazlarda desteklemelidir. Azure AD yararlanan [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |Tamperproof mekanizmaları toohello aygıt Örneğin çok zor tooimpossible tooextract anahtarları ve diğer şifreleme malzeme hello aygıttan yaparak uygulayın. |birisi hello aygıt (fiziksel girişim) oynama, Hello riski oluşturur. Gerçekleştirildiğine nasıl emin olun, bu cihaz üzerinde oynama değil. |Merhaba en etkili Azaltıcı olduğu, hangi hello anahtarları okunamıyor, ancak yalnızca başlangıç anahtarı kullanan ancak hiçbir zaman hello anahtar ifşa şifreleme işlemleri için kullanılan özel yongadaki devresi anahtarlarını depolamak sağlayan bir güvenilir platform Modülü (TPM) özellik . Merhaba aygıt bellek şifreleme. Merhaba cihaz için anahtar yönetimi. Merhaba kod imzalama. | |
| E |Erişim denetimi hello cihazın sahip. Yetkilendirme düzeni. |Merhaba aygıt toobe komutları bir dış kaynaktan dayanan gerçekleştirilen veya hatta algılayıcılar tehlikeye bireysel işlemlere izin veriyorsa, bu hello saldırı tooperform operations aksi erişilebilir izin verir. |Merhaba cihaz için Yetkilendirme düzeni sahip | |
| Alan ağ geçidi |S |Merhaba alan ağ geçidi tooCloud ağ geçidi (bağlı olarak, sertifika PSK, bağlı olarak, talep..) kimlik doğrulaması |Ardından, birisi alan ağ geçidi taklit edebilir, kendisini herhangi bir aygıtı sunabilir. |TLS RSA/PSK, IPSec, [RFC 4279](https://tools.ietf.org/html/rfc4279). Tümü aynı anahtar depolama hello ve aygıtların genel – en iyi durum kanıtlama sorunları TPM kullanın. IPSec toosupport kablosuz algılayıcı ağları (WSN) için 6LowPAN uzantısı. |
| TRID |Merhaba alan ağ geçidi'ne (TPM?) kurcalanmaya karşı koruma |Sahtekarlığı hello bulut ağ geçidi toofield Konuşmayı düşünüyorum kandırarak saldırıları ağ geçidi bilgilerin açığa çıkması ve verileri izinsiz neden olabilir |Bellek şifreleme, TPM bilgisayarın, kimlik doğrulaması. | |
| E |Alan ağ geçidi için erişim denetimi mekanizması | | | |

Bu kategorideki tehditleri bazı örnekleri şunlardır:

Kimlik sahtekarlığı: Bir saldırgan şifreleme anahtar malzemesi bir aygıttan ayıklamak, hello kimlik altında farklı bir fiziksel veya sanal cihaz hello sistemiyle hello aygıt hello anahtar malzeme ya da hello yazılım veya donanım düzeyinde ve daha sonra erişimi alınırlar.

**Hizmet reddi**: bir aygıt çalışmıyor veya radyo frekansları veya kesme kablolarını uğratarak iletişim kuramadığı oluşturulabilir. Örneğin, özellikle gizleyen güç veya ağ bağlantısı olan bir izleme kamera verileri hiç bildirmez.

**İzinsiz**: bir saldırgan hello cihazda çalışan hello yazılım kısmen veya tamamen değiştirebilir, anahtar malzeme veya şifreleme hello hello yerine yazılım tooleverage hello orijinal kimliğini hello aygıt Merhaba, potansiyel olarak izin verme anahtar malzeme bulunduran tesis kullanılabilir toohello yasadışı program yoktu.

**İzinsiz**: boş koridor spektrumun görünür resmini gösteren bir izleme kamera böyle bir koridor fotoğrafı amaçlayan. Duman veya yangın algılayıcı birisi altındaki bir açık tutarak raporlama. Her iki durumda da hello aygıt teknik hello sistem tam olarak güvenilir olabilir, ancak yönetilebilen bilgi rapor eder.

**İzinsiz**: bir saldırgan ayıklanan anahtar malzeme toointercept yararlanan hello iletişim yolunun hello aygıtta verilerden bastırmak ve çalınırsa hello anahtar malzemesi ile kimlik doğrulaması yanlış veri değiştirin.

**İzinsiz**: bir saldırgan hello cihazda çalışan hello yazılım kısmen veya tamamen değiştirebilir, anahtar malzeme veya şifreleme hello hello yerine yazılım tooleverage hello orijinal kimliğini hello aygıt Merhaba, potansiyel olarak izin verme anahtar malzeme bulunduran tesis kullanılabilir toohello yasadışı program yoktu.

**Bilgilerin açığa çıkmasına**: hello cihaz yönetilebilen yazılım çalışıyorsa yönetilebilen yazılımla olası veri toounauthorized tarafların sızıntısı.

**Bilgilerin açığa çıkmasına**: bir saldırgan ayıklanan anahtar malzeme tooinject kendisini hello iletişim yolunun hello aygıt denetleyicisi veya alan ağ geçidi arasında içine yararlanan veya ağ geçidi toosiphon bilgi kapalı bulut.

**Hizmet reddi**: hello aygıt devre dışı ya da bir moduna iletişimi (olduğu birçok endüstriyel makinelerinizde kasıtlı) mümkün olduğu açık.

**İzinsiz**: hello aygıt yeniden yapılandırılan toooperate bir durumda olabilir bilinmeyen toohello kontrol sistem (dışında bilinen ayarlama parametreleri) ve böylece yorumlanabilir verileri sağlar

**Ayrıcalık yükseltme**: belirli bir işlevi gerçekleştiren cihaz zorlanmış toodo başka bir şey olabilir. Örneğin, tüm hello tooopen yarısı şekilde olabilir programlanmış tooopen olan bir Vana sağladı yolu.

**Hizmet reddi**: hello cihaz iletişimi olduğu olası bir duruma açılabilir.

**İzinsiz**: hello aygıt yeniden yapılandırılan toooperate bir durumda olabilir bilinmeyen toohello kontrol sistem (dışında bilinen ayarlama parametreleri) ve böylece yorumlanabilir veriler sağlar.

**Kimlik sahtekarlığı/kurcalama/ret**: Güvenli varsa (olduğu nadiren hello durumu tüketici uzaktan denetimleri ile) bir saldırganın bir aygıtı hello durumunu anonim olarak değiştirebilirsiniz. Uzaktan herhangi TV kapatabilirsiniz ve popüler prankster araçları olan denetimleri buna iyi bir çizimidir.

#### <a name="communication"></a>İletişim
Cihazlar, aygıtları ve alan ağ geçitleri ve cihaz ve bulut ağ geçidi arasındaki iletişim yolunun geçici tehditleri. Merhaba tabloda hello aygıt/VPN açık yuvalarda geçici bazı yönergeler vardır:

| **Bileşen** | **Tehdit** | **Azaltma** | **Riski** | **Uygulama** |
| --- | --- | --- | --- | --- |
| Cihaz IOT hub'ı |KOMUTU |(D) TLS (PSK/RSA) tooencrypt hello trafiği |Gizli dinleme veya hello aygıt hello ağ geçidi arasında hello iletişimi engelliyor |Merhaba protokol düzeyi güvenliği. Özel protokoller ile nasıl toofigure ihtiyacımız tooprotect bunları. Çoğu durumda, hello iletişimi hello aygıt toohello IOT Hub'ın (aygıt hello bağlantı başlatır) yer alır. |
| Aygıtın aygıt |KOMUTU |(D) TLS (PSK/RSA) tooencrypt hello trafiği. |Cihazlar arasında Aktarımdaki verileri okunuyor. Merhaba verilerinize müdahale. Yeni bağlantıları Hello aygıtla aşırı yüklemesi |Güvenlik hello protokol düzeyinde (MQTT/AMQP/HTTP/CoAP. Özel protokoller ile nasıl toofigure ihtiyacımız tooprotect bunları. Merhaba azaltma hello DoS tehdit için bir bulut ya da alan ağ geçidi üzerinden toopeer cihazları ve bunları istemcileri hello ağ doğru olarak yalnızca act sahip. Merhaba eşliği hello ağ geçidiyle aracılı sonra hello eşler arasında doğrudan bağlantı ile sonuçlanabilir |
| Dış varlık cihaz |KOMUTU |Güçlü hello Dış varlık toohello aygıtın eşleştirme |Dinleme hello bağlantı toohello aygıt. Merhaba aygıt ile engellemesini hello iletişim |Güvenli bir şekilde hello Dış varlık toohello aygıt NFC/Bluetooth LE çifti. Merhaba işletimsel hello aygıt (fiziksel) panelinin denetleme |
| Alan ağ geçidi bulut ağ geçidi |KOMUTU |TLS (PSK/RSA) tooencrypt hello trafiği. |Gizli dinleme veya hello aygıt hello ağ geçidi arasında hello iletişimi engelliyor |Güvenlik hello protokol düzeyinde (MQTT/AMQP/HTTP/CoAP). Özel protokoller ile nasıl toofigure ihtiyacımız tooprotect bunları. |
| Cihaz bulut ağ geçidi |KOMUTU |TLS (PSK/RSA) tooencrypt hello trafiği. |Gizli dinleme veya hello aygıt hello ağ geçidi arasında hello iletişimi engelliyor |Güvenlik hello protokol düzeyinde (MQTT/AMQP/HTTP/CoAP). Özel protokoller ile nasıl toofigure ihtiyacımız tooprotect bunları. |

Bu kategorideki tehditleri bazı örnekleri şunlardır:

**Hizmet reddi**: kısıtlanmış aygıtlardır genellikle DoS tehlike altında bir saldırganın birçok bağlantıları paralel olarak açabilir ve değil bunları hizmet veya hizmet çünkü bunlar etkin olarak gelen bağlantıları veya bir ağ üzerindeki istenmeyen veri birimleri için dinlerken bunları çok yavaş veya hello aygıt ile istenmeyen trafiği yayılmamış olabilir. Her iki durumda da hello aygıt etkili bir şekilde hello ağda kullanılamaz hale getirilebilir.

**Yanıltma, bilgi İfşası**: kısıtlanmış aygıtları ve özel amaçlı cihazlar genellikle parola veya PIN koruma gibi tüm için bir güvenlik tesis sahiptir veya bunlar tamamen bunlar erişimine anlamı güvenen hello ağda kullanır bir aygıt üzerinde hello olduğunda tooinformation aynı ağ ve o ağ paylaşılan bir anahtar tarafından korunan genellikle yalnızca. Gizli toodevice hello paylaşılan ya da ağ duyurulmuş olası toocontrol hello aygıt veya hello aygıttan yayılan verileri gözlemlemek anlamına gelir.  

**Kimlik sahtekarlığı**: bir saldırgan müdahale veya kısmen hello yayın ve sızma hello başlatanın (Merhaba ortadaki adam) geçersiz kıl

**İzinsiz**: bir saldırgan müdahale veya kısmen hello yayın geçersiz kılabilir ya da yanlış bilgi gönder 

**Bilgi İfşası:** bir saldırganın bir yayın üzerinde misafiri ve yetkilendirme bilgileri elde **hizmet reddi:** bir saldırganın jam hello yayını sinyal ve bilgi dağıtım Reddet

#### <a name="storage"></a>Depolama
Her cihaz ve alan ağ geçidi (queuing hello verileri için işletim sistemi (OS) görüntüsü depolama geçici) depolama çeşit vardır.

| **Bileşen** | **Tehdit** | **Azaltma** | **Riski** | **Uygulama** |
| --- | --- | --- | --- | --- |
| Cihaz depolama |TRID |Depolama şifrelemesi, Hello günlükleri imzalama |Merhaba depolama (PII veri) verileri telemetri verilerinize müdahale okuma. Değiştirilmesine sıraya veya komut denetim verileri önbelleğe alınmış. Yapılandırma veya bellenimi güncelleştirme paketleriyle oynama önbelleğe alınmış veya yerel olarak kuyruğa sırada güvenliğinin bozulması riskini tooOS ve/veya sistem bileşenleri yol açabilir |Şifreleme, ileti kimlik doğrulama kodu (MAC) veya dijital imza. Burada kaynak erişimi aracılığıyla olası, güçlü erişim denetim listeleri (ACL'ler) veya izinleri denetler. |
| Cihaz işletim sistemi görüntüsü |TRID | |İşletim sistemiyle oynama / hello işletim sistemi bileşenleri değiştirme |Salt okunur işletim sistemi bölümü, imzalı işletim sistemi görüntüsü, şifreleme |
| Alan ağ geçidi depolama (queuing hello veri) |TRID |Depolama şifrelemesi, Hello günlükleri imzalama |Merhaba depolama (PII veri) telemetri verilerinize müdahale verileri okuma, sıraya değiştirilmesine veya komut denetim verileri önbelleğe alınmış. (Aygıtlar veya alan ağ geçidi için hedefleyen) yapılandırması veya bellenimi güncelleştirme paketleriyle oynama önbelleğe alınmış veya yerel olarak kuyruğa sırada güvenliğinin bozulması riskini tooOS ve/veya sistem bileşenleri yol açabilir |BitLocker'ı |
| Alan ağ geçidi işletim sistemi görüntüsü |TRID | |İşletim sistemiyle oynama / hello işletim sistemi bileşenleri değiştirme |Salt okunur işletim sistemi bölümü, imzalı işletim sistemi görüntüsü, şifreleme |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Aygıt ve olay işleme/bulut ağ geçidi bölge
Bulut ağ geçidi genellikle bir bulut tabanlı denetim ve veri analizi sistem, bu sistemlere Federasyonu doğrultusunda ortak ağ alanı üzerinden uzaktan iletişimi ve birkaç farklı sitelerin toodevices veya alan ağ geçitleri sağlayan sistemidir. Bazı durumlarda, bir bulut ağ geçidi hemen erişim toospecial amacı Terminal tabletler veya telefonlar gibi aygıtlardan kolaylaştırabilir. Ele alınan hello bağlamda burada "bulut" aynı sitede hello aygıtları veya alan ağ geçitleri bağlı olarak ve işletimsel ölçüleri önlemek fiziksel erişimi hedeflenen ancak değil ilişkili toohello değil toorefer ayrılmış tooa veri işleme sistem tasarlanmıştır mutlaka tooa "Genel bulut" altyapısı.  Bulut ağ geçidi, ağ sanallaştırma katmana tooinsulate hello bulut ağ geçidi ve tüm bağlı aygıtları veya alan ağ geçitleri üzerinden diğer ağ trafiğinden potansiyel olarak eşlenebilir. Merhaba bulut ağ geçidinin kendisi ne aygıt denetim sistem ya da bir işleme veya depolama tesisi cihaz verileri için olan; Bu olanakları ile Merhaba bulut Ağ Geçidi Arabirimi. Aygıt tooit doğrudan veya dolaylı olarak bağlı ve hello bulut ağ geçidinin tüm alan ağ geçitleri ile birlikte Hello bulut ağ geçidi bölge içerir.

Bulut ağ geçidi genellikle özel yerleşik yazılım sunulma uç noktaları toowhich alan ağ geçidi ile bir hizmet olarak çalışan bir parçasıdır ve aygıtları bağlayın. Bu nedenle ile göz önünde bulundurularak tasarlanmalıdır. Lütfen izleyin [SDL](http://www.microsoft.com/sdl) tasarlama ve bu hizmet oluşturmak için işlem. 

#### <a name="services-zone"></a>Hizmetleri bölge
Bir denetim sistemi (veya denetleyicisi) arabirimleri bir cihaz veya alan ağ geçidi veya Bulut ağ geçidi için bir veya birden çok cihaz ve/veya toocollect ve/veya deposu denetleme hello amacı ve/veya sunu için aygıt verilerini analiz bir yazılım çözümü olan veya izleyen denetim amaçlar. Denetim sistemleri hello yalnızca kişilerle etkileşim hemen kolaylaştırabilir bu tartışma hello kapsamındaki varlıklardır. Merhaba özel durum izin veren bir kişi tooturn hello aygıt devre dışı bir anahtar gibi cihazlarda Ara fiziksel denetim yüzeyleri veya diğer özelliklerini değiştirmek ve kendisi için dijital olarak erişilebilen işlevsel bir eşdeğeri yoktur. 

Ara fiziksel denetim yüzeyleri bilgilerdir burada mantığını yöneten, herhangi bir biçimini kısıtlar hello işlevi hello fiziksel denetim yüzeyinin sağlayacak şekilde eşdeğer bir işlevi uzaktan başlatılabilir veya hükümsüz kılınan – bu tür uzaktan giriş giriş çakışıyor olabilir intermediated denetim yüzeyleri kavramsal olarak ekli tooa yerel denetim sistem aygıt hello herhangi bir uzaktan denetim sistem ekli tooin paralel olabileceğinden yararlanır aynı temel işlevleri hello ' dir. Olabilir, okuma üst tehditleri toohello bulut [bulut güvenlik Alliance (CSA)](https://cloudsecurityalliance.org/research/top-threats/) sayfası.

## <a name="additional-resources"></a>Ek kaynaklar
Makaleler ek bilgi için aşağıdaki toohello bakın:

* [SDL tehdit modelleme aracı](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
* [Microsoft Azure IOT başvuru mimarisi](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

## <a name="see-also"></a>Ayrıca bkz.
IOT çözümünüzün güvenliğini sağlama hakkında daha fazla toolearn bkz [, IOT dağıtımınızın güvenliğini][lnk-security-deployment].

Merhaba bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri ayrıca keşfedebilirsiniz:

* [Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış][lnk-predictive-overview]
* [IoT Paketi için sık sorulan sorular][lnk-faq]

IOT hub'ı güvenlik konusunda okuyabilirsiniz [Denetim erişim tooIoT Hub] [ lnk-devguide-security] hello IOT Hub Geliştirici Kılavuzu'nda.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md